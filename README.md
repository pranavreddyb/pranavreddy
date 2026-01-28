namespace DocumentProcessingApp.Models
{
    public class ExtractedFormDto
    {
        public int Id { get; set; }   // optional (DB identity)

        // ===== FORM 1120 FIELDS =====

        public string EIN { get; set; }

        public string Name { get; set; }

        public string Street { get; set; }

        public string CityStateZip { get; set; }

        public int TaxYear { get; set; }

        public decimal TotalAssets { get; set; }

        public DateTime? DateIncorporated { get; set; }

        public string ECheck { get; set; }
    }
}















