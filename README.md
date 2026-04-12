body {
  font-family: Arial, sans-serif;
  background: #f4f6f8;
  margin: 0;
  padding: 20px;
}

h1 {
  color: #1e3a8a;
  margin-bottom: 20px;
}

h2 {
  color: #374151;
  margin-top: 25px;
}

input {
  padding: 10px;
  margin: 5px;
  width: 220px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
}

input:focus {
  outline: none;
  border-color: #2563eb;
}

button {
  padding: 9px 14px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  color: white;
  margin: 3px;
  font-size: 14px;
}

button:hover {
  opacity: 0.9;
}

button:first-of-type {
  background: #2563eb;
}

table {
  width: 100%;
  margin-top: 15px;
  border-collapse: collapse;
  background: white;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

th {
  background: #1f2937;
  color: white;
  padding: 12px;
}

td {
  padding: 10px;
  border-bottom: 1px solid #e5e7eb;
}

tr:hover {
  background: #f9fafb;
}

.edit-btn,
button:nth-child(1) {
  background: #f59e0b;
}

.delete-btn,
button:nth-child(2) {
  background: #ef4444;
}
