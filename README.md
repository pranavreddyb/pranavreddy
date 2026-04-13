app.ts

import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';
import { EmployeeService } from './employee.service';

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
  editIndex = -1;

  constructor(public employeeService: EmployeeService) {}

  get items() {
    return this.employeeService.getItems();
  }

  add() {
    if (this.name == '' || this.role == '' || this.exp == '') {
      alert('Please fill all fields');
      return;
    }

    const data = {
      name: this.name,
      role: this.role,
      exp: this.exp
    };

    if (this.editIndex == -1) {
      this.employeeService.addItem(data);
    } else {
      this.employeeService.updateItem(this.editIndex, data);
      this.editIndex = -1;
    }

    this.clearFields();
  }

  edit(i: number) {
    this.name = this.items[i].name;
    this.role = this.items[i].role;
    this.exp = this.items[i].exp;
    this.editIndex = i;
  }

  delete(i: number) {
    if (confirm('Are you sure you want to delete this employee?')) {
      this.employeeService.deleteItem(i);
    }
  }

  clearFields() {
    this.name = '';
    this.role = '';
    this.exp = '';
  }
}
