using Microsoft.AspNetCore.Mvc;
using ReadingListApi.Models;
using ReadingListApi.Data;

namespace ReadingListApi.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ReadingItemsController : ControllerBase
    {
        // GET: api/readingitems
        [HttpGet]
        public ActionResult<IEnumerable<ReadingItem>> GetAll()
        {
            return Ok(ReadingItemStore.Items);
        }










using Microsoft.AspNetCore.Mvc;
using ReadingListApi.Models;
using ReadingListApi.Data;

namespace ReadingListApi.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ReadingItemsController : ControllerBase
    {
        // GET: api/readingitems
        [HttpGet]
        public ActionResult<IEnumerable<ReadingItem>> GetAll()
        {
            return Ok(ReadingItemStore.Items);
        }

        // GET: api/readingitems/5
        [HttpGet("{id}")]
        public ActionResult<ReadingItem> GetById(int id)
        {
            var item = ReadingItemStore.Items.FirstOrDefault(x => x.Id == id);

            if (item == null)
                return NotFound("Item not found");

            return Ok(item);
        }

        // POST: api/readingitems
        [HttpPost]
        public ActionResult<ReadingItem> Create(ReadingItem newItem)
        {
            if (string.IsNullOrWhiteSpace(newItem.Title))
                return BadRequest("Title is required");

            newItem.Id = ReadingItemStore.GetNextId();

            if (!IsValidStatus(newItem.Status))
                return BadRequest("Status must be Planned, Reading or Done");

            ReadingItemStore.Items.Add(newItem);

            return CreatedAtAction(nameof(GetById),
                new { id = newItem.Id },
                newItem);
        }

        // PUT: api/readingitems/5
        [HttpPut("{id}")]
        public IActionResult Update(int id, ReadingItem updatedItem)
        {
            var existingItem = ReadingItemStore.Items.FirstOrDefault(x => x.Id == id);

            if (existingItem == null)
                return NotFound("Item not found");

            if (!IsValidStatus(updatedItem.Status))
                return BadRequest("Status must be Planned, Reading or Done");

            existingItem.Title = updatedItem.Title;
            existingItem.Author = updatedItem.Author;
            existingItem.Status = updatedItem.Status;

            return NoContent();
        }

        // DELETE: api/readingitems/5
        [HttpDelete("{id}")]
        public IActionResult Delete(int id)
        {
            var item = ReadingItemStore.Items.FirstOrDefault(x => x.Id == id);

            if (item == null)
                return NotFound("Item not found");

            ReadingItemStore.Items.Remove(item);

            return NoContent();
        }

        private bool IsValidStatus(string status)
        {
            var validStatuses = new[] { "Planned", "Reading", "Done" };
            return validStatuses.Contains(status);
        }
    }
}
