using Azure;
using Azure.AI.FormRecognizer.DocumentAnalysis;

public async Task ProcessDocument(byte[] pdfBytes)
{
    Console.WriteLine("=== ProcessDocument CALLED ===");

    var endpoint = _configuration["ADI:Endpoint"];
    var apiKey = _configuration["ADI:ApiKey"];

    if (string.IsNullOrWhiteSpace(endpoint) || string.IsNullOrWhiteSpace(apiKey))
        throw new Exception("ADI configuration missing");

    var client = new DocumentAnalysisClient(
        new Uri(endpoint),
        new AzureKeyCredential(apiKey)
    );

    using var stream = new MemoryStream(pdfBytes);

    var operation = await client.AnalyzeDocumentAsync(
        WaitUntil.Completed,
        "prebuilt-tax.us.1120",
        stream
    );

    var result = operation.Value;
    var doc = result.Documents.First();

    // ===== REQUIRED 1120 FIELDS =====

    string name =
        doc.Fields.GetValueOrDefault("CorporationName")?.Content;

    string street =
        doc.Fields.GetValueOrDefault("Address")?
            .Value.AsAddress()?.StreetAddress;

    string cityStateZip =
        doc.Fields.GetValueOrDefault("Address")?
            .Value.AsAddress()?.City + ", " +
        doc.Fields.GetValueOrDefault("Address")?
            .Value.AsAddress()?.State + " " +
        doc.Fields.GetValueOrDefault("Address")?
            .Value.AsAddress()?.PostalCode;

    string ein =
        doc.Fields.GetValueOrDefault("EmployerIdentificationNumber")?.Content;

    DateTime? dateIncorporated =
        doc.Fields.GetValueOrDefault("DateIncorporated")?
            .Value.AsDate();

    decimal totalAssets =
        doc.Fields.GetValueOrDefault("TotalAssets")?
            .Value.AsFloat() ?? 0;

    string eCheck =
        doc.Fields.GetValueOrDefault("ElectronicFiling")?.Content;

    int taxYear =
        int.Parse(doc.Fields.GetValueOrDefault("TaxYear")?.Content);

    // ===== SAFETY CHECK =====
    if (string.IsNullOrEmpty(ein))
    {
        Console.WriteLine("EIN NOT FOUND – NOT SAVING");
        return;
    }

    // ===== SAVE TO DB =====
    var dto = new ExtractedFormDto
    {
        EIN = ein,
        Name = name,
        Street = street,
        CityStateZip = cityStateZip,
        DateIncorporated = dateIncorporated,
        TaxYear = taxYear,
        TotalAssets = totalAssets,
        ECheck = eCheck
    };

    _repository.Insert(dto);

    Console.WriteLine("=== FORM 1120 DATA SAVED ===");
}















