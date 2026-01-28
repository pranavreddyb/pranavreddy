var endpoint = _configuration["ADI:Endpoint"];
var apiKey = _configuration["ADI:ApiKey"];

var client = new DocumentAnalysisClient(
    new Uri(endpoint),
    new AzureKeyCredential(apiKey)
);

using var stream = new MemoryStream(pdfBytes);

var operation = await client.AnalyzeDocumentAsync(
    WaitUntil.Completed,
    "prebuilt-document",
    stream
);

AnalyzeResult result = operation.Value;
string text = result.Content;









