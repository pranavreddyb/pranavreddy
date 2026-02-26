using Microsoft.AspNetCore.Mvc;
using ReadingListApi.Models;

namespace ReadingListApi.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ReadingItemsController : ControllerBase
    {
        private static List<ReadingItem> items = new List<ReadingItem>();
        private static int nextId = 1;

        // GET: api/readingitems
        [HttpGet]
        public ActionResult<IEnumerable<ReadingItem>> GetAll()
        {
            return Ok(items);
        }

        // GET: api/readingitems/1
        [HttpGet("{id}")]
        public ActionResult<ReadingItem> GetById(int id)
        {
            var item = items.FirstOrDefault(x => x.Id == id);

            if (item == null)
                return NotFound();

            return Ok(item);
        }

        // POST: api/readingitems
        [HttpPost]
        public ActionResult<ReadingItem> Create(ReadingItem newItem)
        {
            newItem.Id = nextId++;
            items.Add(newItem);

            return CreatedAtAction(nameof(GetById),
                new { id = newItem.Id },
                newItem);
        }

        // PUT: api/readingitems/1
        [HttpPut("{id}")]
        public IActionResult Update(int id, ReadingItem updatedItem)
        {
            var item = items.FirstOrDefault(x => x.Id == id);

            if (item == null)
                return NotFound();

            item.Title = updatedItem.Title;
            item.Author = updatedItem.Author;
            item.Status = updatedItem.Status;

            return NoContent();
        }

        // DELETE: api/readingitems/1
        [HttpDelete("{id}")]
        public IActionResult Delete(int id)
        {
            var item = items.FirstOrDefault(x => x.Id == id);

            if (item == null)
                return NotFound();

            items.Remove(item);

            return NoContent();
        }
    }
}
