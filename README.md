employee.service.ts

import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class EmployeeService {
  items: any[] = [];

  getItems() {
    return this.items;
  }

  addItem(data: any) {
    this.items.push(data);
  }

  updateItem(index: number, data: any) {
    this.items[index] = data;
  }

  deleteItem(index: number) {
    this.items.splice(index, 1);
  }
}
