import { Component, OnInit } from '@angular/core';
import { Router } from '@angular/router';
import { FormsModule } from '@angular/forms';
import { CommonModule } from '@angular/common';
import { Modal } from '../modal/modal';
import { EmployeeService } from '../../employee.service';

@Component({
  selector: 'app-employee-list',
  standalone: true,
  imports: [FormsModule, CommonModule, Modal],
  templateUrl: './employee-list.html',
  styleUrl: './employee-list.css'
})
export class EmployeeList implements OnInit {

  items: any[] = [];

  name = '';
  role = '';
  exp = '';
  email = '';
  department = '';
  location = '';

  editIndex = -1;
  showModal = false;
  modalTitle = '';
  modalMessage = '';
  modalType = 'alert';
  deleteIndex = -1;

  originalData: any = null;

  constructor(
    public employeeService: EmployeeService,
    private router: Router
  ) {}

  ngOnInit() {
    this.loadEmployees();
  }

  loadEmployees() {
    this.employeeService.getItems().subscribe((data: any) => {
      this.items = data;
    });
  }

  add() {
    if (!this.name || !this.role || !this.exp || !this.email || !this.department || !this.location) {
      this.modalTitle = 'Validation';
      this.modalMessage = 'Please fill all fields.';
      this.modalType = 'alert';
      this.showModal = true;
      return;
    }

    const data = {
      name: this.name,
      role: this.role,
      exp: this.exp,
      email: this.email,
      department: this.department,
      location: this.location
    };

    if (this.editIndex === -1) {
      this.employeeService.addItem(data).subscribe(() => {
        this.loadEmployees();
        this.clearFields();
      });
    } else {
      this.employeeService.updateItem(this.editIndex, data).subscribe(() => {
        this.loadEmployees();
        this.clearFields();
        this.editIndex = -1;
      });
    }
  }

  edit(i: number) {
    const item = this.items[i];

    this.name = item.name;
    this.role = item.role;
    this.exp = item.exp;
    this.email = item.email;
    this.department = item.department;
    this.location = item.location;

    this.originalData = { ...item };
    this.editIndex = i;
  }

  delete(i: number) {
    this.deleteIndex = i;
    this.modalTitle = 'Delete Employee';
    this.modalMessage = 'Are you sure you want to delete this employee?';
    this.modalType = 'confirm';
    this.showModal = true;
  }

  confirmDelete() {
    this.employeeService.deleteItem(this.deleteIndex).subscribe(() => {
      this.loadEmployees();
      this.showModal = false;
    });
  }

  viewDetails(i: number) {
    this.router.navigate(['/details', i]);
  }

  clearFields() {
    this.name = '';
    this.role = '';
    this.exp = '';
    this.email = '';
    this.department = '';
    this.location = '';
  }
}
