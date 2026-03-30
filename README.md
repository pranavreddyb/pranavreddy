<h2>Add Experience</h2>

<div class="input-group">
  <input #expInput type="text" placeholder="Describe your experience...">
  <button (click)="addExperience(expInput.value); expInput.value=''">
    Add
  </button>
</div>
