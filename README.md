using System;
using System.IO;
using System.Linq;
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
            Console.WriteLine("=== ProcessDocument STARTED ===");

            // 🔹 Read ADI config
            var endpoint = _configuration["ADI:Endpoint"];
            var apiKey = _configuration["ADI:ApiKey"];

            if (string.IsNullOrEmpty(endpoint) || string.IsNullOrEmpty(apiKey))
                throw new Exception("ADI configuration missing");

            // 🔹 Create ADI client
            var client = new DocumentAnalysisClient(
                new Uri(endpoint),
                new AzureKeyCredential(apiKey)
            );

            using var stream = new MemoryStream(pdfBytes);

            // 🔹 Call ADI (prebuilt-document)
            var operation = await client.AnalyzeDocumentAsync(
                WaitUntil.Completed,
                "prebuilt-document",
                stream
            );

            var result = operation.Value;

            // 🔹 Get first document
            var document = result.Documents.FirstOrDefault();
            if (document == null)
            {
                Console.WriteLine("❌ No document detected");
                return;
            }

            var fields = document.Fields;

            // 🔹 Helper to safely read fields
            string GetField(string key)
            {
                if (fields.ContainsKey(key))
                    return fields[key]?.Content;
                return null;
            }

            // ===============================
            // ✅ FORM 1120 FIELD MAPPING
            // ===============================
            var dto = new ExtractedFormDto
            {
                CompanyName = GetField("Name"),
                EIN = GetField("EmployerIdentificationNumber"),
                Street = GetField("Address"),
                CityStateZip = GetField("CityStateZip"),

                TaxYear = int.TryParse(GetField("TaxYear"), out var taxYear)
                            ? taxYear
                            : 0,

                TotalAssets = decimal.TryParse(
                                    GetField("TotalAssets")?.Replace(",", ""),
                                    out var assets)
                                ? assets
                                : 0,

                DateIncorporated = DateTime.TryParse(
                                        GetField("DateIncorporated"),
                                        out var date)
                                    ? date
                                    : null,

                ECheck = GetField("ECheck")
            };

            // 🔹 Save to database
            _repository.Insert(dto);

            Console.WriteLine("✅ DATA SAVED TO DATABASE");
            Console.WriteLine("=== ProcessDocument FINISHED ===");
        }
    }
}
