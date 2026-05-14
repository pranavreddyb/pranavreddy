import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-debrief',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './debrief.html',
  styleUrl: './debrief.css'
})
export class Debrief {
  feedback = {
    overallScore: 8.5,
    strengths: [
      'Clearly described the performance issue.',
      'Used respectful and professional language.',
      'Invited the employee to share their perspective.'
    ],
    improvements: [
      'Ask more open-ended questions.',
      'Summarize agreed next steps.',
      'Confirm accountability and deadlines.'
    ],
    nextSteps:
      'Schedule a follow-up meeting in two weeks to review progress.'
  };
}
