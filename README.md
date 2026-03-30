import { Component } from '@angular/core';
import { CommonModule } from '@angular/common';
import { ExpService } from '../exp.service';

@Component({
  selector: 'app-list-exp',
  standalone: true,
  imports: [CommonModule],
  templateUrl: './list-exp.html',
  styleUrl: './list-exp.css'
})
export class ListExpComponent {

  constructor(public expService: ExpService) {}

}
