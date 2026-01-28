// STEP 1: Call Azure Document Intelligence (ADI)

var endpoint = _configuration["ADI:Endpoint"];
var apiKey = _configuration["ADI:ApiKey"];

var client = new DocumentIntelligenceClient(
    new Uri(endpoint),
    new AzureKeyCredential(apiKey)
);

using var stream = new MemoryStream(pdfBytes);

var operation = client.AnalyzeDocument(
    WaitUntil.Completed,
    "prebuilt-document",
    stream
);

var result = operation.Value;





