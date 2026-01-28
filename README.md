using Microsoft.AspNetCore.Mvc;
using DocumentProcessingApp.Services;

namespace DocumentProcessingApp.Controllers
{
    public class UploadController : Controller
    {
        private readonly DocumentService _service;

        public UploadController(DocumentService service)
        {
            _service = service;
        }

        [HttpGet]
        public IActionResult Upload()
        {
            return View();
        }

        [HttpPost]
        public async Task<IActionResult> Upload(IFormFile file)
        {
            if (file == null || file.Length == 0)
                return BadRequest("Invalid file");

            using var ms = new MemoryStream();
            await file.CopyToAsync(ms);

            // 🔴 PROOF THIS METHOD IS CALLED
            Console.WriteLine("UPLOAD CONTROLLER: File received");
            Console.WriteLine($"File size: {ms.Length}");

            // 🔴 THIS LINE MUST RUN
            await _service.ProcessDocument(ms.ToArray());

            Console.WriteLine("UPLOAD CONTROLLER: ProcessDocument finished");

            return Ok("File processed and saved to SQL");
        }
    }
}










