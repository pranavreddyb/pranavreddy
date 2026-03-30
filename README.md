<h2>Add Experience</h2>

<input #expInput type="text" placeholder="Enter experience">
<button (click)="addExperience(expInput.value); expInput.value=''">
  Add
</button>
