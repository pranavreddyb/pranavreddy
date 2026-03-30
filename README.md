<div *ngFor="let exp of experiences">
  <ul>
    <li *ngFor="let line of getFormattedList(exp)">
      {{ line }}
    </li>
  </ul>

  <button class="delete-btn" (click)="deleteExperience(exp)">
    Delete
  </button>

  <hr>
</div>
