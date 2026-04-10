<h1>CRUD Application</h1>

<h2>Add Employee</h2>

<input [(ngModel)]="name" placeholder="Name">
<input [(ngModel)]="role" placeholder="Role">
<input [(ngModel)]="exp" placeholder="Experience">

<button (click)="add()">Add</button>

<hr>

<h2>Employee List</h2>

<table border="1">
  <tr>
    <th>Name</th>
    <th>Role</th>
    <th>Experience</th>
  </tr>

  <tr *ngFor="let item of items">
    <td>{{item.name}}</td>
    <td>{{item.role}}</td>
    <td>{{item.exp}}</td>
  </tr>
</table>
