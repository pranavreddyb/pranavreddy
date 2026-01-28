@{
    ViewData["Title"] = "Upload Document";
}

<h2>Upload PDF</h2>

<form asp-controller="Upload"
      asp-action="Upload"
      method="post"
      enctype="multipart/form-data">

    <input type="file" name="file" accept=".pdf" required />
    <br /><br />

    <button type="submit">Upload</button>
</form>



