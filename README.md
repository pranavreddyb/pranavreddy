import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class ExpService {

  private experiences: string[] = [];

  addExperience(exp: string) {
    this.experiences.push(exp);
  }

  getExperiences() {
    return this.experiences;
  }
}
