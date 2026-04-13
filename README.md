app.css

body {
  margin: 0;
  padding: 45px 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
  min-height: 100vh;
  background: linear-gradient(135deg, #0f172a, #1e293b, #111827);
}

.container {
  max-width: 1350px;
  margin: auto;
  padding: 34px;
  border-radius: 28px;
  background: #f8fafc;
  box-shadow: 0 30px 60px rgba(0,0,0,0.35);
}

h1 {
  margin: 0 0 28px;
  text-align: center;
  font-size: 38px;
  font-weight: 800;
  color: #111827;
}

h2 {
  margin: 28px 0 14px;
  font-size: 22px;
  font-weight: 700;
  color: #1e293b;
}

.form-box {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  padding: 18px;
  border-radius: 18px;
  background: #e2e8f0;
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 14px 16px;
  border: 1px solid #cbd5e1;
  border-radius: 12px;
  background: white;
  font-size: 14px;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 4px rgba(37,99,235,0.15);
}

button {
  border: none;
  border-radius: 12px;
  padding: 14px 20px;
  min-width: 115px;
  font-size: 14px;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: 0.25s;
}

button:hover {
  transform: translateY(-2px);
}

.form-box button {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
}

.edit-btn {
  background: linear-gradient(135deg, #f59e0b, #ea580c);
  margin-right: 8px;
}

.delete-btn {
  background: linear-gradient(135deg, #ef4444, #dc2626);
}

table {
  width: 100%;
  margin-top: 22px;
  border-collapse: separate;
  border-spacing: 0;
  overflow: hidden;
  border-radius: 18px;
  background: white;
}

th {
  background: linear-gradient(135deg, #111827, #374151);
  color: white;
  padding: 16px;
  text-align: left;
}

td {
  padding: 15px;
  color: #334155;
  border-bottom: 1px solid #e5e7eb;
}

tr:nth-child(even) td {
  background: #f8fafc;
}

tr:hover td {
  background: #dbeafe;
}

p {
  margin-top: 18px;
  padding: 16px;
  border-radius: 14px;
  background: #e0f2fe;
  color: #0369a1;
  text-align: center;
  font-weight: 600;
}

@media (max-width: 768px) {
  .container {
    padding: 20px;
  }

  h1 {
    font-size: 30px;
  }

  button {
    width: 100%;
  }
}
