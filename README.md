<mat-card class="chat-container">
  <!-- Messages Area -->
  <div class="messages">
    <div
      *ngFor="let message of messages"
      class="message"
      [class.user]="message.sender === 'user'"
      [class.ai]="message.sender === 'ai'"
    >
      <strong>{{ message.sender === 'user' ? 'You' : 'AI' }}:</strong>
      {{ message.text }}
    </div>

    <!-- Loading Spinner -->
    <div class="loading" *ngIf="loading">
      <mat-spinner diameter="30"></mat-spinner>
    </div>
  </div>

  <!-- Input Area -->
  <div class="input-area">
    <mat-form-field appearance="outline" class="input-field">
      <textarea
        matInput
        rows="2"
        [(ngModel)]="userInput"
        placeholder="Type your message..."
        (keydown.enter)="sendMessage(); $event.preventDefault()"
      ></textarea>
    </mat-form-field>

    <button
      mat-raised-button
      color="primary"
      (click)="sendMessage()"
      [disabled]="loading"
    >
      Send
    </button>
  </div>
</mat-card>
