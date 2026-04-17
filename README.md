const data = {
  name: this.name,
  role: this.role,
  exp: this.exp,
  email: this.email,
  department: this.department,
  location: this.location
};

if (this.editIndex !== -1) {
  const sameData =
    this.name === this.originalData.name &&
    this.role === this.originalData.role &&
    this.exp === this.originalData.exp &&
    this.email === this.originalData.email &&
    this.department === this.originalData.department &&
    this.location === this.originalData.location;

  if (sameData) {
    alert('Please change at least one field before updating');
    return;
  }
}

if (this.editIndex === -1) {
  this.employeeService.addItem(data);
} else {
  this.employeeService.updateItem(this.editIndex, data);
  this.editIndex = -1;
}
