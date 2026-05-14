import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { Router } from '@angular/router';
import { inject } from '@angular/core';

import { Chat, ChatMessage } from '../../shared/chat/chat';

@Component({
  selector: 'app-roleplay',
  standalone: true,
  imports: [CommonModule, Chat],
  templateUrl: './roleplay.html',
  styleUrl: './roleplay.css'
})
export class Roleplay {
  private router = inject(Router);

  messages: ChatMessage[] = [
    {
      sender: 'ai',
      text: 'I am ready to role-play as your employee. Start the conversation whenever you are ready.'
    }
  ];

  loading = false;

  onMessageSent(message: string): void {
    // Add manager's message
    this.messages.push({
      sender: 'user',
      text: message
    });

    // Simulate employee response for now
    this.loading = true;

    setTimeout(() => {
      this.messages.push({
        sender: 'ai',
        text: 'I understand your concerns. Can you explain what specific issues you noticed?'
      });

      this.loading = false;
    }, 1500);
  }

  goToDebrief(): void {
    this.router.navigate(['/debrief']);
  }
}
