import { Component, Input, Output, EventEmitter } from '@angular/core';
import { CommonModule } from '@angular/common';

@Component({
  selector: 'app-modal',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './modal.html',
  styleUrls: ['./modal.css']
})
export class Modal {

  @Input() show: boolean = false;
  @Input() title: string = '';
  @Input() message: string = '';
  @Input() type: string = '';

  @Output() close = new EventEmitter<void>();
  @Output() confirmAction = new EventEmitter<void>();

  closeModal() {
    this.close.emit();
  }

  confirm() {
    this.confirmAction.emit();
  }
}
