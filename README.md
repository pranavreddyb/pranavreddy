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
      const formatted = this.formatExperience(value); // 👈 uses function
      this.expService.addExperience(formatted);
    }
  }

  // 👇 PASTE STEP 1 HERE
  formatExperience(exp: string): string {

    const text = exp.toLowerCase();

    if (text.includes('project')) {
      return `Developed and delivered multiple projects
Applied practical knowledge in real-world scenarios
Strengthened problem-solving and debugging skills`;
    }

    if (text.includes('ai') || text.includes('machine learning')) {
      return `Worked on AI/ML concepts and implementations
Gained hands-on experience with intelligent systems
Improved analytical and data-driven thinking`;
    }

    if (text.includes('intern')) {
      return `Completed internship with practical exposure
Collaborated with team members on tasks
Learned industry-level workflows`;
    }

    return `Worked on ${exp}
Gained hands-on experience in ${exp}
Improved problem-solving skills`;
  }
}
