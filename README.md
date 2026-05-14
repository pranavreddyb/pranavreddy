<div class="debrief-page">
  <h1>Coaching Debrief</h1>

  <h2>Overall Score: {{ feedback.overallScore }}/10</h2>

  <h3>Strengths</h3>
  <ul>
    <li *ngFor="let item of feedback.strengths">
      {{ item }}
    </li>
  </ul>

  <h3>Areas for Improvement</h3>
  <ul>
    <li *ngFor="let item of feedback.improvements">
      {{ item }}
    </li>
  </ul>

  <h3>Recommended Next Steps</h3>
  <p>{{ feedback.nextSteps }}</p>
</div>
