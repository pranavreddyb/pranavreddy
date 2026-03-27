template: `
  <h1>User Manager</h1>

  <input [(ngModel)]="name" placeholder="Enter name">
  <button (click)="addUser()">Add</button>

  <ul>
    <li *ngFor="let user of users">
      {{ user }}
      <button (click)="deleteUser(user)">Delete</button>
    </li>
  </ul>
`,
