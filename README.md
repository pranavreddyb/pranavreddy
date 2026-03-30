<h2>Experience List</h2>

<ul>
  <li *ngFor="let exp of expService.experiences; let i = index">
    <pre>{{ exp }}</pre>
    <button (click)="expService.removeExperience(i)">Delete</button>
  </li>
</ul>
