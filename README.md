import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class EmployeeService {

  apiUrl = 'http://127.0.0.1:8000/employees';

  constructor(private http: HttpClient) {}

  getItems() {
    return this.http.get<any[]>(this.apiUrl);
  }

  addItem(data: any) {
    return this.http.post(this.apiUrl, data);
  }

  updateItem(id: number, data: any) {
    return this.http.put(`${this.apiUrl}/${id}`, data);
  }

  deleteItem(id: number) {
    return this.http.delete(`${this.apiUrl}/${id}`);
  }
}
