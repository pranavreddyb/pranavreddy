using Microsoft.Data.SqlClient;
using Microsoft.Extensions.Configuration;
using DocumentProcessingApp.Models;

namespace DocumentProcessingApp.Repositories
{
    public class ExtractedDataRepository
    {
        private readonly string _connectionString;

        public ExtractedDataRepository(IConfiguration configuration)
        {
            _connectionString = configuration.GetConnectionString("DefaultConnection");
        }

        public void Insert(ExtractedFormDto dto)
        {
            using var conn = new SqlConnection(_connectionString);
            conn.Open();

            var cmd = new SqlCommand(@"
                INSERT INTO ExtractedData
                (CompanyName, Street, CityStateZip, EIN, TaxYear, TotalAssets, DateIncorporated, ECheck)
                VALUES
                (@CompanyName, @Street, @CityStateZip, @EIN, @TaxYear, @TotalAssets, @DateIncorporated, @ECheck)
            ", conn);

            cmd.Parameters.AddWithValue("@CompanyName", (object?)dto.CompanyName ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@Street", (object?)dto.Street ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@CityStateZip", (object?)dto.CityStateZip ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@EIN", (object?)dto.EIN ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@TaxYear", dto.TaxYear);
            cmd.Parameters.AddWithValue("@TotalAssets", dto.TotalAssets);
            cmd.Parameters.AddWithValue("@DateIncorporated", (object?)dto.DateIncorporated ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@ECheck", (object?)dto.ECheck ?? DBNull.Value);

            cmd.ExecuteNonQuery();
        }
    }
}





















