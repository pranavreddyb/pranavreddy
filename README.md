import { Component } from '@angular/core';
import { Router } from '@angular/router';
import { EmployeeService } from '../../employee.service';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-employee-list',
  standalone: true,
  imports: [FormsModule, CommonModule],
  templateUrl: './employee-list.html',
  styleUrl: './employee-list.css'
})
export class EmployeeList {

  name = '';
  role = '';
  exp = '';
  editIndex = -1;

  constructor(
    public employeeService: EmployeeService,
    private router: Router
  ) {}

  get items() {
    return this.employeeService.getItems();
  }

  add() {
    if (!this.name || !this.role || !this.exp) {
      alert('Please fill all fields');
      return;
    }

    const data = {
      name: this.name,
      role: this.role,
      exp: this.exp
    };

    if (this.editIndex === -1) {
      this.employeeService.addItem(data);
    } else {
      this.employeeService.updateItem(this.editIndex, data);
      this.editIndex = -1;
    }

    this.clearFields();
  }

  edit(i: number) {
    const item = this.items[i];
    this.name = item.name;
    this.role = item.role;
    this.exp = item.exp;
    this.editIndex = i;
  }

  delete(i: number) {
    if (confirm('Are you sure to delete?')) {
      this.employeeService.deleteItem(i);
    }
  }

  viewDetails(i: number) {
    this.router.navigate(['/details', i]);
  }

  clearFields() {
    this.name = '';
    this.role = '';
    this.exp = '';
  }
}
