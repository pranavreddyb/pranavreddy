app.html

<div class="container">

  <h1>CRUD Application</h1>

  <h2>Add Employee</h2>

  <div class="form-box">
    <input [(ngModel)]="name" placeholder="Name">
    <input [(ngModel)]="role" placeholder="Role">
    <input [(ngModel)]="exp" placeholder="Experience">

    <button (click)="add()">
      {{ editIndex == -1 ? 'Add' : 'Update' }}
    </button>
  </div>

  <h2>Employee List</h2>

  <p *ngIf="items.length == 0">No employees added yet.</p>

  <table *ngIf="items.length > 0">
    <tr>
      <th>ID</th>
      <th>Name</th>
      <th>Role</th>
      <th>Experience</th>
      <th>Action</th>
    </tr>

    <tr *ngFor="let item of items; let i = index">
      <td>{{ i + 1 }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.role }}</td>
      <td>{{ item.exp }}</td>
      <td>
        <button class="edit-btn" (click)="edit(i)">Edit</button>
        <button class="delete-btn" (click)="delete(i)">Delete</button>
      </td>
    </tr>
  </table>

</div>
