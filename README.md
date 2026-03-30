import { Component } from '@angular/core';
import { AddExpComponent } from './add-exp/add-exp.component';
import { ListExpComponent } from './list-exp/list-exp.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [AddExpComponent, ListExpComponent],
  templateUrl: './app.html'
})
export class AppComponent {}
