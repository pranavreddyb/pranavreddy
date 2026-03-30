<h2>Add Experience</h2>

<input type="text" placeholder="Enter experience" #expInput>

<button (click)="addExperience(expInput.value)">
  Add
</button>

<ul>
  <li *ngFor="let exp of experiences">
    {{ exp }}
  </li>
</ul>
