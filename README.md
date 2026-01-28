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
        public IActionResult Upload(IFormFile file)
        {
            if (file == null || file.Length == 0)
                return BadRequest("Invalid file");

            using var ms = new MemoryStream();
            file.CopyTo(ms);

            _service.ProcessDocument(ms.ToArray());

            return Ok("File processed and saved to SQL");
        }
    }
}




