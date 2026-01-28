using System;
using System.IO;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using Microsoft.Extensions.Configuration;
using Azure;
using Azure.AI.FormRecognizer.DocumentAnalysis;
using DocumentProcessingApp.Models;
using DocumentProcessingApp.Repositories;

namespace DocumentProcessingApp.Services
{
    public class DocumentService
    {
        private readonly IConfiguration _configuration;
        private readonly ExtractedDataRepository _repository;

        public DocumentService(
            IConfiguration configuration,
            ExtractedDataRepository repository)
        {
            _configuration = configuration;
            _repository = repository;
        }

        public async Task ProcessDocument(byte[] pdfBytes)
        {
            Console.WriteLine("=== ProcessDocument CALLED ===");

            // ---------- READ CONFIG ----------
            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            Console.WriteLine($"ADI ENDPOINT: {endpoint}");
            Console.WriteLine($"ADI API KEY EXISTS: {!string.IsNullOrEmpty(apiKey)}");

            if (string.IsNullOrEmpty(endpoint) || string.IsNullOrEmpty(apiKey))
                throw new Exception("ADI config missing in appsettings.json");

            // ---------- CREATE CLIENT ----------
            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey)
            );

            // ---------- SEND PDF ----------
            using var stream = new MemoryStream(pdfBytes);

            AnalyzeDocumentOperation operation =
                await client.AnalyzeDocumentAsync(
                    WaitUntil.Completed,
                    "prebuilt-document",
                    stream
                );

            AnalyzeResult result = operation.Value;

            // ---------- OCR TEXT ----------
            string text = result.Content;

            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // 🔴 DEBUG FILE (MUST EXIST)
            Directory.CreateDirectory(@"C:\temp");
            File.WriteAllText(@"C:\temp\ocr.txt", text);

            // ---------- EIN EXTRACTION ----------
            var einMatch = Regex.Match(
                text,
                @"\b\d{2}[-\s]?\d{7}\b"
            );

            if (!einMatch.Success)
            {
                Console.WriteLine("❌ EIN NOT FOUND — NOT SAVING");
                return;
            }

            string ein = einMatch.Value.Replace("-", "").Replace(" ", "");
            Console.WriteLine($"✅ EIN FOUND: {ein}");

            // ---------- TOTAL ASSETS EXTRACTION ----------
            var assetsMatch = Regex.Match(
                text,
                @"Total\s+Assets.*?([\d,]+)",
                RegexOptions.IgnoreCase | RegexOptions.Singleline
            );

            decimal totalAssets = 0;

            if (assetsMatch.Success)
            {
                decimal.TryParse(
                    assetsMatch.Groups[1].Value.Replace(",", ""),
                    out totalAssets
                );
            }

            Console.WriteLine($"✅ TOTAL ASSETS: {totalAssets}");

            // ---------- SAVE TO DB ----------
            var dto = new ExtractedFormDto
            {
                EIN = ein,
                TaxYear = DateTime.Now.Year,
                TotalAssets = totalAssets
            };

            _repository.Insert(dto);

            Console.WriteLine("✅ DATA SAVED TO DATABASE");
        }
    }
}














