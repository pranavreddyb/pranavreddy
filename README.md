
<h2>Experience List</h2>

<div *ngFor="let exp of experiences" class="card">

  <ul>
    <li *ngFor="let line of getFormattedList(exp)">
      {{ line }}
    </li>
  </ul>

  <button class="delete-btn" (click)="deleteExperience(exp)">
    Delete
  </button>

</div>
