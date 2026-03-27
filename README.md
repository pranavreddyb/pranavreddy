import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [FormsModule, CommonModule],
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
})
export class AppComponent {
  name: string = '';
  users: string[] = [];

  addUser() {
    if (this.name.trim()) {
      this.users.push(this.name);
      this.name = '';
    }
  }

  deleteUser(user: string) {
    this.users = this.users.filter(u => u !== user);
  }
}
