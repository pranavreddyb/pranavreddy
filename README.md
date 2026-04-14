<div class="container">
  <h1>CRUD Application</h1>

  <h3>Add Employee</h3>

  <div class="form-row">
    <input type="text" placeholder="Name" [(ngModel)]="name">
    <input type="text" placeholder="Role" [(ngModel)]="role">
    <input type="text" placeholder="Experience" [(ngModel)]="exp">
    <button class="add-btn" (click)="add()">
      {{ editIndex === -1 ? 'Add' : 'Update' }}
    </button>
  </div>

  <h3>Employee List</h3>

  <table class="employee-table" *ngIf="items.length > 0">
    <tr>
      <th>Name</th>
      <th>Role</th>
      <th>Experience</th>
      <th>Action</th>
    </tr>

    <tr *ngFor="let item of items; let i = index">
      <td>{{ item.name }}</td>
      <td>{{ item.role }}</td>
      <td>{{ item.exp }}</td>
      <td>
        <button class="view-btn" (click)="viewDetails(i)">View</button>
        <button class="edit-btn" (click)="edit(i)">Edit</button>
        <button class="delete-btn" (click)="delete(i)">Delete</button>
      </td>
    </tr>
  </table>

  <p *ngIf="items.length === 0">No employees found</p>
</div>
