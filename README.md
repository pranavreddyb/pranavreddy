import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class ExpService {

  experiences: string[] = [];

  addExperience(exp: string) {
    const formatted = this.formatExperience(exp);
    this.experiences.push(formatted);
  }

  getExperiences() {
    return this.experiences;
  }

  removeExperience(index: number) {
    this.experiences.splice(index, 1);
  }

  formatExperience(exp: string): string {
    return `• Worked on ${exp}
• Gained hands-on experience in ${exp}
• Improved problem-solving skills`;
  }
}
