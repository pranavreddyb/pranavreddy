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

            // 🔑 Read ADI config
            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            Console.WriteLine($"ADI ENDPOINT: {endpoint}");
            Console.WriteLine($"ADI API KEY EXISTS: {!string.IsNullOrEmpty(apiKey)}");

            if (string.IsNullOrEmpty(endpoint) || string.IsNullOrEmpty(apiKey))
                throw new Exception("ADI config missing in appsettings.json");

            // 🤖 Azure Document Intelligence client
            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey)
            );

            using var stream = new MemoryStream(pdfBytes);

            // 📄 Analyze PDF
            AnalyzeDocumentOperation operation =
                await client.AnalyzeDocumentAsync(
                    WaitUntil.Completed,
                    "prebuilt-document",
                    stream
                );

            AnalyzeResult result = operation.Value;

            string text = result.Content;

            // 🔍 PRINT OCR TEXT (VERY IMPORTANT)
            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // ===== EXTRACT EIN =====
            string ein = Regex.Match(
                text,
                @"Employer Identification Number[:\s]*([\d\s-]{9,})",
                RegexOptions.IgnoreCase
            ).Groups[1].Value.Replace(" ", "").Replace("-", "");

            // ===== EXTRACT TOTAL ASSETS =====
            string assetsRaw = Regex.Match(
                text,
                @"Total\s+Assets[:\s]*([\d,]+)",
                RegexOptions.IgnoreCase
            ).Groups[1].Value;

            decimal.TryParse(
                assetsRaw.Replace(",", ""),
                out decimal totalAssets
            );

            // ❌ STOP if data not found
            if (string.IsNullOrWhiteSpace(ein))
            {
                Console.WriteLine("❌ EIN NOT FOUND — NOT SAVING");
                return;
            }

            if (totalAssets == 0)
            {
                Console.WriteLine("❌ TOTAL ASSETS NOT FOUND — NOT SAVING");
                return;
            }

            // ✅ SAVE TO DB
            var dto = new ExtractedFormDto
            {
                EIN = ein,
                TaxYear = DateTime.Now.Year,
                TotalAssets = totalAssets
            };

            _repository.Insert(dto);

            Console.WriteLine("=== DATA SAVED TO DATABASE ===");
        }
    }
}












