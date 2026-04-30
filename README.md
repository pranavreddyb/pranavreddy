import { Component, OnInit } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { EmployeeService } from '../../employee.service';
import { Modal } from '../modal/modal';

@Component({
  selector: 'app-employee-list',
  standalone: true,
  imports: [CommonModule, FormsModule, Modal],
  templateUrl: './employee-list.html',
  styleUrls: ['./employee-list.css']
})
export class EmployeeList implements OnInit {

  items: any[] = [];

  // form
  name = '';
  role = '';
  exp = '';
  email = '';
  department = '';
  location = '';

  editIndex = -1;

  // modal
  showModal = false;
  modalTitle = '';
  modalMessage = '';
  modalType = '';
  deleteIndex = -1;

  constructor(private employeeService: EmployeeService) {}

  ngOnInit() {
    this.loadEmployees();
  }

  loadEmployees() {
    this.employeeService.getEmployees().subscribe(data => {
      this.items = data;
    });
  }

  save() {
    if (!this.name || !this.role || !this.exp || !this.email) {
      alert('Fill required fields');
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
      this.employeeService.addEmployee(data).subscribe(() => {
        this.loadEmployees();
        this.clear();
      });
    } else {
      this.employeeService.updateEmployee(this.editIndex, data).subscribe(() => {
        this.loadEmployees();
        this.clear();
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
    this.editIndex = i;
  }

  delete(i: number) {
    this.deleteIndex = i;
    this.modalTitle = 'Delete Employee';
    this.modalMessage = 'Are you sure?';
    this.modalType = 'confirm';
    this.showModal = true;
  }

  confirmDelete() {
    this.employeeService.deleteEmployee(this.deleteIndex).subscribe(() => {
      this.loadEmployees();
      this.showModal = false;
    });
  }

  closeModal() {
    this.showModal = false;
  }

  clear() {
    this.name = '';
    this.role = '';
    this.exp = '';
    this.email = '';
    this.department = '';
    this.location = '';
    this.editIndex = -1;
  }

  viewDetails(i: number) {
    const item = this.items[i];
    this.modalTitle = item.name;
    this.modalMessage = `${item.role} - ${item.email}`;
    this.modalType = 'alert';
    this.showModal = true;
  }
}
