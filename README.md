import { Component } from '@angular/core';
import { AddExpComponent } from './add-exp/add-exp';
import { ListExpComponent } from './list-exp/list-exp';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [AddExpComponent, ListExpComponent],
  templateUrl: './app.html',
  styleUrl: './app.css'
})
export class AppComponent {}
