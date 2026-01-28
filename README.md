var endpoint = _configuration["ADI:Endpoint"];
var apiKey = _configuration["ADI:ApiKey"];

var client = new DocumentIntelligenceClient(
    new Uri(endpoint),
    new AzureKeyCredential(apiKey)
);

using var stream = new MemoryStream(pdfBytes);

// ✅ THIS is the correct call for your SDK
var operation = client.AnalyzeDocumentAsync(
    WaitUntil.Completed,
    "prebuilt-document",
    stream
).Result;

var result = operation.Value;






