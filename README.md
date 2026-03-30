import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { ExpService } from '../exp.service';

@Component({
  selector: 'app-list-exp',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './list-exp.html',
  styleUrl: './list-exp.css'
})
export class ListExpComponent {

  experiences: string[] = []; // 👈 THIS WAS MISSING

  constructor(private expService: ExpService) {
    this.experiences = this.expService.getExperiences();
  }

  getFormattedList(exp: string): string[] {
    return exp.split('\n');
  }

  deleteExperience(exp: string) {
    this.experiences = this.experiences.filter(e => e !== exp);
  }
}
