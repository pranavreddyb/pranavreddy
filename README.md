import { Injectable, inject } from '@angular/core';
import { HttpClient } from '@angular/common/http';

@Injectable({
  providedIn: 'root'
})
export class CoachingApi {
  // Get Angular's HttpClient using the inject() function
  private http = inject(HttpClient);

  // Base URL of the backend server
  private baseUrl = 'http://localhost:8000';

  // Create a new coaching session
  createSession() {
    return this.http.post<{ session_id: string }>(
      `${this.baseUrl}/sessions`,
      {}
    );
  }

  // Send a user message to the backend
  sendMessage(sessionId: string, message: string) {
    return this.http.post<{ response: string }>(
      `${this.baseUrl}/sessions/${sessionId}/message`,
      {
        message
      }
    );
  }

  // Retrieve the generated coaching plan
  getCoachingPlan(sessionId: string) {
    return this.http.get<any>(
      `${this.baseUrl}/sessions/${sessionId}/plan`
    );
  }
}
