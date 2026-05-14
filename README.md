<div class="planning-page">
  <h1>Coaching Plan Preparation</h1>

  <app-chat
    [messages]="messages"
    [loading]="loading"
    (messageSent)="onMessageSent($event)">
  </app-chat>

  <div class="actions" *ngIf="planReady">
    <button mat-raised-button color="primary" (click)="loadPlan()">
      View Full Plan
    </button>

    <button mat-raised-button color="accent" (click)="startRoleplay()">
      Start Role-Play
    </button>
  </div>

  <pre *ngIf="coachingPlan">{{ coachingPlan | json }}</pre>
</div>
