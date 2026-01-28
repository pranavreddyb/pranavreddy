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

            // 🔹 Read ADI config
            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            Console.WriteLine($"ADI ENDPOINT: {endpoint}");
            Console.WriteLine($"ADI API KEY EXISTS: {!string.IsNullOrEmpty(apiKey)}");

            if (string.IsNullOrWhiteSpace(endpoint) || string.IsNullOrWhiteSpace(apiKey))
                throw new Exception("ADI config missing in appsettings.json");

            // 🔹 Create Azure client
            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey)
            );

            using var stream = new MemoryStream(pdfBytes);

            // 🔹 Call Azure OCR
            AnalyzeDocumentOperation operation =
                await client.AnalyzeDocumentAsync(
                    WaitUntil.Completed,
                    "prebuilt-document",
                    stream
                );

            AnalyzeResult result = operation.Value;

            string text = result.Content ?? string.Empty;

            Console.WriteLine("=== OCR TEXT START ===");
            Console.WriteLine(text);
            Console.WriteLine("=== OCR TEXT END ===");

            // ===============================
            // FORM 1120 DATA EXTRACTION
            // ===============================

            // EIN (XX-XXXXXXX)
            string ein = Regex.Match(text, @"\b\d{2}-\d{7}\b").Value;

            // Tax Year (4 digits near “Tax year”)
            int taxYear = DateTime.Now.Year;
            var taxYearMatch = Regex.Match(text, @"Tax\s*Year\s*(20\d{2})");
            if (taxYearMatch.Success)
                taxYear = int.Parse(taxYearMatch.Groups[1].Value);

            // Total Assets
            decimal totalAssets = 0;
            var assetsMatch = Regex.Match(
                text,
                @"Total\s+assets\s*\$?\s*([\d,]+)",
                RegexOptions.IgnoreCase
            );

            if (assetsMatch.Success)
            {
                decimal.TryParse(
                    assetsMatch.Groups[1].Value.Replace(",", ""),
                    out totalAssets
                );
            }

            // Company Name (first big text block heuristic)
            string companyName = Regex.Match(
                text,
                @"(?m)^\s*([A-Z][A-Z\s,&\.]{3,})\s*$"
            ).Value;

            // Address line
            string street = Regex.Match(
                text,
                @"\d+.+(Street|St|Road|Rd|Avenue|Ave|Blvd).*",
                RegexOptions.IgnoreCase
            ).Value;

            // City / State / ZIP
            string cityStateZip = Regex.Match(
                text,
                @"[A-Z][a-zA-Z\s]+,\s*[A-Z]{2}\s*\d{5}",
                RegexOptions.IgnoreCase
            ).Value;

            // Date incorporated
            DateTime? dateIncorporated = null;
            var dateMatch = Regex.Match(
                text,
                @"Date\s+incorporated\s*(\d{1,2}/\d{1,2}/\d{4})",
                RegexOptions.IgnoreCase
            );

            if (dateMatch.Success &&
                DateTime.TryParse(dateMatch.Groups[1].Value, out var parsedDate))
            {
                dateIncorporated = parsedDate;
            }

            // E-Check flag
            string eCheck = Regex.IsMatch(text, @"E-?Check", RegexOptions.IgnoreCase)
                ? "Yes"
                : "No";

            Console.WriteLine("=== EXTRACTED VALUES ===");
            Console.WriteLine($"EIN: {ein}");
            Console.WriteLine($"TaxYear: {taxYear}");
            Console.WriteLine($"TotalAssets: {totalAssets}");
            Console.WriteLine($"CompanyName: {companyName}");

            // 🔹 Build DTO
            var dto = new ExtractedFormDto
            {
                EIN = ein,
                TaxYear = taxYear,
                TotalAssets = totalAssets,
                CompanyName = companyName,
                Street = street,
                CityStateZip = cityStateZip,
                DateIncorporated = dateIncorporated,
                ECheck = eCheck
            };

            // 🔹 Save to DB
            _repository.Insert(dto);

            Console.WriteLine("=== DATA SAVED TO DATABASE ===");
        }
    }
}



















