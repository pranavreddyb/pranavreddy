import { Component, EventEmitter, Input, Output } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { MatCardModule } from '@angular/material/card';
import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';
import { MatProgressSpinnerModule } from '@angular/material/progress-spinner';

export interface ChatMessage {
  sender: 'user' | 'ai';
  text: string;
}

@Component({
  selector: 'app-chat',
  standalone: true,
  imports: [
    CommonModule,
    FormsModule,
    MatCardModule,
    MatButtonModule,
    MatInputModule,
    MatProgressSpinnerModule
  ],
  templateUrl: './chat.html',
  styleUrl: './chat.css'
})
export class Chat {
  @Input() messages: ChatMessage[] = [];
  @Input() loading = false;

  @Output() messageSent = new EventEmitter<string>();

  userInput = '';

  sendMessage(): void {
    const text = this.userInput.trim();

    if (!text) {
      return;
    }

    this.messageSent.emit(text);
    this.userInput = '';
  }
}
