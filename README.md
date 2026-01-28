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
            using var connection = new SqlConnection(_connectionString);
            connection.Open();

            var sql = @"
                INSERT INTO ExtractedData
                (EIN, TaxYear, TotalAssets, CompanyName, Street, CityStateZip, DateIncorporated, ECheck)
                VALUES
                (@EIN, @TaxYear, @TotalAssets, @CompanyName, @Street, @CityStateZip, @DateIncorporated, @ECheck)
            ";

            using var cmd = new SqlCommand(sql, connection);

            cmd.Parameters.AddWithValue("@EIN", dto.EIN);
            cmd.Parameters.AddWithValue("@TaxYear", dto.TaxYear);
            cmd.Parameters.AddWithValue("@TotalAssets", dto.TotalAssets);
            cmd.Parameters.AddWithValue("@CompanyName", (object?)dto.CompanyName ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@Street", (object?)dto.Street ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@CityStateZip", (object?)dto.CityStateZip ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@DateIncorporated", (object?)dto.DateIncorporated ?? DBNull.Value);
            cmd.Parameters.AddWithValue("@ECheck", (object?)dto.ECheck ?? DBNull.Value);

            cmd.ExecuteNonQuery();

            Console.WriteLine("✅ DATA INSERTED INTO SQL");
        }
    }
}


















