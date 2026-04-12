app.css

body {
  margin: 0;
  padding: 20px;
  background: #f4f6f8;
  font-family: Arial, sans-serif;
}

.container {
  max-width: 1200px;
  margin: auto;
}

h1 {
  color: #1e3a8a;
  margin-bottom: 20px;
}

h2 {
  color: #374151;
  margin-top: 25px;
  margin-bottom: 15px;
}

.form-box {
  display: flex;
  gap: 10px;
  flex-wrap: wrap;
  align-items: center;
}

input {
  padding: 10px;
  width: 220px;
  border: 1px solid #d1d5db;
  border-radius: 6px;
  font-size: 14px;
}

input:focus {
  outline: none;
  border-color: #2563eb;
}

input::placeholder {
  color: #9ca3af;
}

button {
  padding: 10px 16px;
  min-width: 90px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  color: white;
  background: #2563eb;
  font-size: 14px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

button:hover {
  opacity: 0.9;
}

.edit-btn {
  background: #f59e0b;
  margin-right: 5px;
}

.delete-btn {
  background: #ef4444;
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
  text-align: left;
}

td {
  padding: 12px;
  border-bottom: 1px solid #e5e7eb;
}

tr:hover {
  background: #f9fafb;
}

p {
  color: #6b7280;
  margin-top: 10px;
}
