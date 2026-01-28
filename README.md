using Azure;
using Azure.AI.FormRecognizer.DocumentAnalysis;
using Microsoft.Extensions.Configuration;
using System.Text.RegularExpressions;
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

            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            if (string.IsNullOrEmpty(endpoint) || string.IsNullOrEmpty(apiKey))
                throw new Exception("ADI config missing");

            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey));

            using var stream = new MemoryStream(pdfBytes);

            var operation = await client.AnalyzeDocumentAsync(
                WaitUntil.Completed,
                "prebuilt-document",
                stream);

            var text = operation.Value.Content;

            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // ===== REGEX EXTRACTION =====
            var dto = new ExtractedFormDto
            {
                CompanyName = Regex.Match(text, @"(?i)Name\s*:\s*(.+)").Groups[1].Value,
                Street = Regex.Match(text, @"(?i)Address\s*:\s*(.+)").Groups[1].Value,
                CityStateZip = Regex.Match(text, @"(?i)City.*ZIP\s*:\s*(.+)").Groups[1].Value,
                EIN = Regex.Match(text, @"\b\d{2}-\d{7}\b").Value,
                TaxYear = int.TryParse(
                    Regex.Match(text, @"Tax\s*Year\s*(\d{4})").Groups[1].Value,
                    out int y) ? y : DateTime.Now.Year,
                TotalAssets = decimal.TryParse(
                    Regex.Match(text, @"Total\s+assets\s+([\d,]+)").Groups[1].Value.Replace(",", ""),
                    out decimal a) ? a : 0,
                ECheck = Regex.Match(text, @"E-?Check\s*(Yes|No)", RegexOptions.IgnoreCase).Groups[1].Value
            };

            if (!string.IsNullOrEmpty(dto.EIN))
            {
                _repository.Insert(dto);
                Console.WriteLine("=== DATA SAVED TO DATABASE ===");
            }
            else
            {
                Console.WriteLine("=== EIN NOT FOUND — NOT SAVING ===");
            }
        }
    }
}






















