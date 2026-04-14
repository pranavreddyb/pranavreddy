<div class="details-card" *ngIf="employee">
  <h1>Employee Details</h1>

  <p><strong>Name:</strong> {{ employee.name }}</p>
  <p><strong>Role:</strong> {{ employee.role }}</p>
  <p><strong>Experience:</strong> {{ employee.exp }}</p>

  <button (click)="goBack()">Back</button>
</div>
