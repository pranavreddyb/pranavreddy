app.ts

import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [FormsModule, CommonModule],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class App {
  name = '';
  role = '';
  exp = '';

  items: any[] = [];

  editIndex = -1;

  add() {
    if (this.name == '' || this.role == '' || this.exp == '') {
      alert('Please fill all fields');
      return;
    }

    if (this.editIndex == -1) {
      this.items.push({
        name: this.name,
        role: this.role,
        exp: this.exp
      });
    } else {
      this.items[this.editIndex].name = this.name;
      this.items[this.editIndex].role = this.role;
      this.items[this.editIndex].exp = this.exp;

      this.editIndex = -1;
    }

    this.name = '';
    this.role = '';
    this.exp = '';
  }

  edit(i: number) {
    this.name = this.items[i].name;
    this.role = this.items[i].role;
    this.exp = this.items[i].exp;

    this.editIndex = i;
  }

  delete(i: number) {
    if (confirm('Are you sure to delete?')) {
      this.items.splice(i, 1);
    }
  }
}
