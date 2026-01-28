var endpoint = _configuration["ADI:Endpoint"];
var apiKey = _configuration["ADI:ApiKey"];

var client = new DocumentIntelligenceClient(
    new Uri(endpoint),
    new AzureKeyCredential(apiKey)
);

using var stream = new MemoryStream(pdfBytes);

// ✅ THIS IS THE CORRECT OVERLOAD FOR YOUR SDK
var operation = await client.AnalyzeDocumentAsync(
    WaitUntil.Completed,
    "prebuilt-document",
    stream
);

var result = operation.Value;








