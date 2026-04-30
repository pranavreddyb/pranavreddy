import { Component, OnInit } from '@angular/core';
import { CommonModule } from '@angular/common';
import { EmployeeService } from '../../employee.service';
import { Modal } from '../modal/modal';

@Component({
  selector: 'app-employee-list',
  standalone: true,
  imports: [CommonModule, Modal],
  templateUrl: './employee-list.html',
  styleUrl: './employee-list.css'
})
export class EmployeeList implements OnInit {

  items: any[] = [];

  // modal variables
  showModal: boolean = false;
  modalTitle: string = '';
  modalMessage: string = '';
  modalType: string = 'alert';

  deleteIndex: number = -1;

  constructor(private employeeService: EmployeeService) {}

  ngOnInit() {
    this.loadEmployees();
  }

  loadEmployees() {
    this.employeeService.getEmployees().subscribe((data: any) => {
      this.items = data;
    });
  }

  // ✅ VIEW DETAILS
  viewDetails(index: number) {
    const item = this.items[index];

    this.modalTitle = 'Employee Details';
    this.modalMessage =
      'Name: ' + item.name + '\n' +
      'Role: ' + item.role + '\n' +
      'Email: ' + item.email + '\n' +
      'Department: ' + item.department + '\n' +
      'Location: ' + item.location;

    this.modalType = 'alert';
    this.showModal = true;
  }

  // ✅ EDIT (basic placeholder)
  edit(index: number) {
    alert('Edit clicked for: ' + this.items[index].name);
  }

  // ✅ DELETE CLICK
  delete(index: number) {
    this.deleteIndex = index;

    this.modalTitle = 'Delete Employee';
    this.modalMessage = 'Are you sure you want to delete this employee?';
    this.modalType = 'confirm';
    this.showModal = true;
  }

  // ✅ CONFIRM DELETE
  confirmDelete() {
    this.employeeService.deleteEmployee(this.deleteIndex).subscribe(() => {
      this.loadEmployees();
      this.showModal = false;
    });
  }

}
