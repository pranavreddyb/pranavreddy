import { Routes } from '@angular/router';
import { PlanningComponent } from './pages/planning/planning.component';
import { RoleplayComponent } from './pages/roleplay/roleplay.component';
import { DebriefComponent } from './pages/debrief/debrief.component';

export const routes: Routes = [
  { path: '', redirectTo: 'plan', pathMatch: 'full' },
  { path: 'plan', component: PlanningComponent },
  { path: 'roleplay', component: RoleplayComponent },
  { path: 'debrief', component: DebriefComponent }
];
