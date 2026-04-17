<div class="container">

  <div class="header">
    <h1>CRUD Application</h1>
    <p>Premium Employee Management Dashboard</p>
  </div>

  <div class="dashboard">

    <!-- Sidebar -->
    <div class="sidebar">
      <h3>Menu</h3>
      <div class="menu-item active">Employees</div>
      <div class="menu-item">Analytics</div>
      <div class="menu-item">Settings</div>
    </div>

    <!-- Main Content -->
    <div class="main-content">

      <!-- Stats -->
      <div class="stats">
        <div class="stat-card">
          <span>Total Employees</span>
          <h2>{{ items.length }}</h2>
        </div>

        <div class="stat-card">
          <span>Departments</span>
          <h2>{{ getDepartmentCount() }}</h2>
        </div>
      </div>

      <!-- Form -->
      <div class="form-box">
        <h3>{{ editIndex === -1 ? 'Add Employee' : 'Update Employee' }}</h3>

        <div class="form-row">
          <input type="text" placeholder="Name" [(ngModel)]="name">
          <input type="text" placeholder="Role" [(ngModel)]="role">
          <input type="text" placeholder="Experience" [(ngModel)]="exp">
          <input type="text" placeholder="Email" [(ngModel)]="email">
          <input type="text" placeholder="Department" [(ngModel)]="department">
          <input type="text" placeholder="Location" [(ngModel)]="location">

          <button class="add-btn" (click)="add()">
            {{ editIndex === -1 ? 'Add Employee' : 'Update Employee' }}
          </button>
        </div>
      </div>

      <!-- Table -->
      <div class="table-box">
        <h3>Employee List</h3>

        <table class="employee-table">
          <thead>
            <tr>
              <th>Name</th>
              <th>Role</th>
              <th>Experience</th>
              <th>Email</th>
              <th>Department</th>
              <th>Location</th>
              <th>Action</th>
            </tr>
          </thead>

          <tbody>
            <tr *ngFor="let item of items; let i = index">
              <td>{{ item.name }}</td>
              <td>{{ item.role }}</td>
              <td>{{ item.exp }}</td>
              <td>{{ item.email }}</td>
              <td>{{ item.department }}</td>
              <td>{{ item.location }}</td>
              <td>
                <button class="view-btn" (click)="viewDetails(i)">View</button>
                <button class="edit-btn" (click)="edit(i)">Edit</button>
                <button class="delete-btn" (click)="delete(i)">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>

        <p *ngIf="items.length === 0">No employees added yet.</p>
      </div>

    </div>
  </div>
</div>
