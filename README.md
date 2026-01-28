using var stream = new MemoryStream(pdfBytes);

// ✅ CORRECT for your SDK
var options = new AnalyzeDocumentOptions(
    modelId: "prebuilt-document",
    document: stream
);

var operation = await client.AnalyzeDocumentAsync(
    WaitUntil.Completed,
    options
);

var result = operation.Value;







