import { Component, OnInit } from '@angular/core';
import { EmployeeService } from '../../employee.service';

@Component({
  selector: 'app-employee-list',
  templateUrl: './employee-list.html',
  styleUrls: ['./employee-list.css']
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

  constructor(private employeeService: EmployeeService) {}

  ngOnInit() {
    this.loadEmployees();
  }

  // LOAD
  loadEmployees() {
    this.employeeService.getEmployees().subscribe(data => {
      this.items = data;
    });
  }

  // ADD or UPDATE
  save() {
    if (!this.name || !this.role || !this.exp || !this.email) {
      alert("Fill required fields");
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

  // EDIT
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

  // DELETE
  delete(i: number) {
    if (confirm("Delete employee?")) {
      this.employeeService.deleteEmployee(i).subscribe(() => {
        this.loadEmployees();
      });
    }
  }

  // CLEAR FORM
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
