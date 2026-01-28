using System;
using System.IO;
using System.Text.RegularExpressions;
using System.Threading.Tasks;
using Azure;
using Azure.AI.FormRecognizer.DocumentAnalysis;
using Microsoft.Extensions.Configuration;
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
                new AzureKeyCredential(apiKey)
            );

            using var stream = new MemoryStream(pdfBytes);

            var operation = await client.AnalyzeDocumentAsync(
                WaitUntil.Completed,
                "prebuilt-document",
                stream
            );

            var result = operation.Value;
            string text = result.Content;

            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // ===== FIELD EXTRACTION (FORM 1120 SPECIFIC) =====

            string companyName = Regex.Match(
                text,
                @"Name\s*\n\s*(.+)",
                RegexOptions.IgnoreCase
            ).Groups[1].Value.Trim();

            string street = Regex.Match(
                text,
                @"Number, street.*?\n\s*(.+)",
                RegexOptions.IgnoreCase
            ).Groups[1].Value.Trim();

            string cityStateZip = Regex.Match(
                text,
                @"City or town.*?\n\s*(.+)",
                RegexOptions.IgnoreCase
            ).Groups[1].Value.Trim();

            string ein = Regex.Match(
                text,
                @"\b\d{2}-\d{7}\b"
            ).Value;

            string taxYearRaw = Regex.Match(
                text,
                @"For calendar year\s*(\d{4})",
                RegexOptions.IgnoreCase
            ).Groups[1].Value;

            int.TryParse(taxYearRaw, out int taxYear);

            string assetsRaw = Regex.Match(
                text,
                @"Total assets.*?\$?\s*([\d,]+\.\d{2})",
                RegexOptions.IgnoreCase
            ).Groups[1].Value;

            decimal.TryParse(
                assetsRaw.Replace(",", ""),
                out decimal totalAssets
            );

            DateTime? dateIncorporated = null;
            var dateMatch = Regex.Match(
                text,
                @"Date incorporated\s*([\d/]+)",
                RegexOptions.IgnoreCase
            );
            if (dateMatch.Success)
                dateIncorporated = DateTime.Parse(dateMatch.Groups[1].Value);

            string eCheck = Regex.IsMatch(text, @"E-?Check", RegexOptions.IgnoreCase)
                ? "YES"
                : "NO";

            var dto = new ExtractedFormDto
            {
                CompanyName = companyName,
                Street = street,
                CityStateZip = cityStateZip,
                EIN = ein,
                TaxYear = taxYear,
                TotalAssets = totalAssets,
                DateIncorporated = dateIncorporated,
                ECheck = eCheck
            };

            _repository.Insert(dto);

            Console.WriteLine("=== DATA SAVED TO DATABASE ===");
        }
    }
}























