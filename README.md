import { Component, OnInit } from '@angular/core';
import { EmployeeService } from '../../employee.service';

@Component({
  selector: 'app-employee-list',
  templateUrl: './employee-list.html',
  styleUrls: ['./employee-list.css']
})
export class EmployeeList implements OnInit {

  items: any[] = [];

  // form fields
  name: string = '';
  role: string = '';
  exp: string = '';
  email: string = '';
  department: string = '';
  location: string = '';

  // edit
  editIndex: number = -1;

  // modal
  showModal: boolean = false;
  deleteIndex: number = -1;

  constructor(private employeeService: EmployeeService) {}

  ngOnInit() {
    this.loadEmployees();
  }

  // 🔹 LOAD EMPLOYEES
  loadEmployees() {
    this.employeeService.getEmployees().subscribe(data => {
      this.items = data;
    });
  }

  // 🔹 ADD OR UPDATE
  save() {
    if (!this.name || !this.role || !this.exp || !this.email) {
      alert("Please fill required fields");
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
      // ADD
      this.employeeService.addEmployee(data).subscribe(() => {
        this.loadEmployees();
        this.clear();
      });
    } else {
      // UPDATE
      this.employeeService.updateEmployee(this.editIndex, data).subscribe(() => {
        this.loadEmployees();
        this.clear();
      });
    }
  }

  // 🔹 EDIT
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

  // 🔹 DELETE (open modal)
  delete(i: number) {
    this.deleteIndex = i;
    this.showModal = true;
  }

  // 🔹 CONFIRM DELETE
  confirmDelete() {
    if (this.deleteIndex !== -1) {
      this.employeeService.deleteEmployee(this.deleteIndex).subscribe(() => {
        this.loadEmployees();
        this.showModal = false;
        this.deleteIndex = -1;
      });
    }
  }

  // 🔹 CLOSE MODAL
  closeModal() {
    this.showModal = false;
    this.deleteIndex = -1;
  }

  // 🔹 CLEAR FORM
  clear() {
    this.name = '';
    this.role = '';
    this.exp = '';
    this.email = '';
    this.department = '';
    this.location = '';
    this.editIndex = -1;
  }
}
