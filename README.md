using System;
using System.IO;
using System.Text.RegularExpressions;
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
        private readonly IExtractedDataRepository _repository;

        public DocumentService(
            IConfiguration configuration,
            IExtractedDataRepository repository)
        {
            _configuration = configuration;
            _repository = repository;
        }

        public async Task ProcessDocument(byte[] pdfBytes)
        {
            Console.WriteLine("=== ProcessDocument CALLED ===");

            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            Console.WriteLine($"ADI ENDPOINT: {endpoint}");
            Console.WriteLine($"ADI API KEY EXISTS: {!string.IsNullOrEmpty(apiKey)}");

            if (string.IsNullOrEmpty(endpoint) || string.IsNullOrEmpty(apiKey))
                throw new Exception("ADI config missing in appsettings.json");

            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey)
            );

            using var stream = new MemoryStream(pdfBytes);

            AnalyzeDocumentOperation operation =
                await client.AnalyzeDocumentAsync(
                    WaitUntil.Completed,
                    "prebuilt-document",
                    stream
                );

            AnalyzeResult result = operation.Value;

            string text = result.Content;
            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // ===== EXTRACT DATA FROM PDF TEXT =====
            string ein = Regex.Match(text, @"\b\d{2}-?\d{7}\b").Value;

            string assetsRaw = Regex.Match(
                text,
                @"Total Assets\s*([\d,]+)",
                RegexOptions.IgnoreCase
            ).Groups[1].Value;

            decimal.TryParse(
                assetsRaw.Replace(",", ""),
                out decimal totalAssets
            );

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











