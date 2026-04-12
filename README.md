<h1>CRUD Application</h1>

<h2>Add Employee</h2>

<input [(ngModel)]="name" placeholder="Name">
<input [(ngModel)]="role" placeholder="Role">
<input [(ngModel)]="exp" placeholder="Experience">

<button (click)="add()">
  {{ editIndex == -1 ? 'Add' : 'Update' }}
</button>

<hr>

<h2>Employee List</h2>

<table border="1">
  <tr>
    <th>Name</th>
    <th>Role</th>
    <th>Experience</th>
    <th>Action</th>
  </tr>

  <tr *ngFor="let item of items; let i = index">
    <td>{{item.name}}</td>
    <td>{{item.role}}</td>
    <td>{{item.exp}}</td>

    <td>
      <button (click)="edit(i)">Edit</button>
      <button (click)="delete(i)">Delete</button>
    </td>
  </tr>
</table>
