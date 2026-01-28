using DocumentProcessingApp.Models;
using DocumentProcessingApp.Repositories;

namespace DocumentProcessingApp.Services
{
    public class DocumentService
    {
        private readonly ExtractedDataRepository _repository;

        public DocumentService(ExtractedDataRepository repository)
        {
            _repository = repository;
        }

        public void ProcessDocument(byte[] pdfBytes)
        {
            // STEP 1: Mock ADI output (for now)
            var adiData = new Dictionary<string, string>
            {
                { "EIN", "12 3456789" },
                { "TotalAssets", "1,000,000" }
            };

            // STEP 2: Normalize data
            string ein = adiData["EIN"].Replace(" ", "");
            decimal totalAssets = decimal.Parse(
                adiData["TotalAssets"].Replace(",", "")
            );

            // STEP 3: Create DTO
            var dto = new ExtractedFormDto
            {
                EIN = ein,
                TaxYear = 2024,
                TotalAssets = totalAssets
            };

            // STEP 4: Send DTO to repository
            _repository.Insert(dto);
        }
    }
}

