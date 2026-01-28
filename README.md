using System.Data.SqlClient;
using DocumentProcessingApp.Models;
using Microsoft.Extensions.Configuration;

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

            var query = @"INSERT INTO ExtractedData (EIN, TaxYear, TotalAssets)
                          VALUES (@EIN, @TaxYear, @TotalAssets)";

            using var command = new SqlCommand(query, connection);
            command.Parameters.AddWithValue("@EIN", dto.EIN);
            command.Parameters.AddWithValue("@TaxYear", dto.TaxYear);
            command.Parameters.AddWithValue(
                "@TotalAssets",
                dto.TotalAssets.HasValue ? dto.TotalAssets.Value : DBNull.Value
            );

            connection.Open();
            command.ExecuteNonQuery();
        }
    }
}


