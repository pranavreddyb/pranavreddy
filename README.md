<div class="overlay" *ngIf="show">
  <div class="modal-box">

    <h2>{{ title }}</h2>
    <p>{{ message }}</p>

    <div class="buttons">

      <button class="cancel-btn" (click)="closeModal()">
        {{ type === 'confirm' ? 'Cancel' : 'OK' }}
      </button>

      <button
        *ngIf="type === 'confirm'"
        class="confirm-btn"
        (click)="confirm()">
        Confirm
      </button>

    </div>

  </div>
</div>
