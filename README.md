app.css

body {
  margin: 0;
  padding: 40px 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
  min-height: 100vh;
  background: linear-gradient(135deg, #0f172a, #1e293b, #111827);
}

.container {
  max-width: 1280px;
  margin: auto;
  background: #ffffff;
  padding: 32px;
  border-radius: 20px;
  box-shadow: 0 20px 45px rgba(0,0,0,0.22);
}

h1 {
  margin: 0 0 28px;
  text-align: center;
  font-size: 34px;
  font-weight: 800;
  color: #111827;
}

h2 {
  margin: 26px 0 14px;
  font-size: 20px;
  font-weight: 700;
  color: #1f2937;
}

.form-box {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  align-items: stretch;
}

input,
button {
  height: 48px;
  box-sizing: border-box;
  border-radius: 12px;
  font-size: 14px;
}

input {
  padding: 0 14px;
  border: 1px solid #d1d5db;
  color: #111827;
  background: #ffffff;
}

input::placeholder {
  color: #6b7280;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 4px rgba(37,99,235,0.12);
}

button {
  border: none;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: 0.2s ease;
}

button:hover {
  transform: translateY(-1px);
}

.form-box button {
  background: #2563eb;
}

.edit-btn {
  background: #f59e0b;
  min-width: 90px;
  margin-right: 8px;
}

.delete-btn {
  background: #ef4444;
  min-width: 90px;
}

table {
  width: 100%;
  margin-top: 20px;
  border-collapse: collapse;
  background: #ffffff;
  border-radius: 14px;
  overflow: hidden;
}

th {
  background: #111827;
  color: white;
  text-align: left;
  padding: 14px;
  font-size: 14px;
}

td {
  padding: 16px 14px;
  border-bottom: 1px solid #e5e7eb;
  color: #374151;
}

tr:hover {
  background: #f9fafb;
}

p {
  margin-top: 16px;
  padding: 14px;
  border-radius: 12px;
  background: #eff6ff;
  color: #1d4ed8;
  text-align: center;
  font-weight: 600;
}

@media (max-width: 768px) {
  .container {
    padding: 20px;
  }

  h1 {
    font-size: 28px;
  }

  .form-box {
    grid-template-columns: 1fr;
  }

  .edit-btn,
  .delete-btn,
  .form-box button {
    width: 100%;
    margin-right: 0;
    margin-bottom: 8px;
  }
}
