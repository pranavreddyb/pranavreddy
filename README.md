<div class="roleplay-page">
  <h1>Role-Play Practice</h1>

  <app-chat
    [messages]="messages"
    [loading]="loading"
    (messageSent)="onMessageSent($event)">
  </app-chat>

  <div class="actions">
    <button mat-raised-button color="primary" (click)="goToDebrief()">
      Finish and View Debrief
    </button>
  </div>
</div>
