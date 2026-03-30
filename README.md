import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { ExpService } from '../exp.service';

@Component({
  selector: 'app-add-exp',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './add-exp.html',
  styleUrl: './add-exp.css'
})
export class AddExpComponent {

  constructor(private expService: ExpService) {}

  addExperience(value: string) {
    if (value) {
      this.expService.addExperience(value);
    }
  }
}
