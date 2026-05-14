import { Component, OnInit, inject } from '@angular/core';
import { CommonModule } from '@angular/common';
import { Router } from '@angular/router';

import { Chat, ChatMessage } from '../../shared/chat/chat';
import { CoachingApi } from '../../services/coaching-api';

@Component({
  selector: 'app-planning',
  standalone: true,
  imports: [CommonModule, Chat],
  templateUrl: './planning.html',
  styleUrl: './planning.css'
})
export class Planning implements OnInit {
  // Inject services
  private api = inject(CoachingApi);
  private router = inject(Router);

  // State variables
  messages: ChatMessage[] = [
    {
      sender: 'ai',
      text: 'Hello! Describe the coaching situation you would like help preparing for.'
    }
  ];

  sessionId = '';
  loading = false;
  coachingPlan: any = null;
  planReady = false;

  // Runs automatically when the page is created
  ngOnInit(): void {
    this.api.createSession().subscribe({
      next: (response) => {
        this.sessionId = response.session_id;
      },
      error: (error) => {
        console.error('Failed to create session:', error);
      }
    });
  }

  // Called when Chat emits messageSent
  onMessageSent(message: string): void {
    // Add user message to chat
    this.messages.push({
      sender: 'user',
      text: message
    });

    // Show loading spinner
    this.loading = true;

    // Send message to backend
    this.api.sendMessage(this.sessionId, message).subscribe({
      next: (response) => {
        // Add AI response
        this.messages.push({
          sender: 'ai',
          text: response.response
        });

        // Temporary condition to enable buttons
        if (response.response.toLowerCase().includes('plan ready')) {
          this.planReady = true;
        }

        this.loading = false;
      },
      error: (error) => {
        console.error('Failed to send message:', error);

        this.messages.push({
          sender: 'ai',
          text: 'Unable to reach the backend.'
        });

        this.loading = false;
      }
    });
  }

  // Fetch the full coaching plan
  loadPlan(): void {
    this.api.getCoachingPlan(this.sessionId).subscribe({
      next: (plan) => {
        this.coachingPlan = plan;
      },
      error: (error) => {
        console.error('Failed to load plan:', error);
      }
    });
  }

  // Navigate to the Roleplay page
  startRoleplay(): void {
    this.router.navigate(['/roleplay']);
  }
}
