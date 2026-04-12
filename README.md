app.css

body {
  margin: 0;
  padding: 30px;
  font-family: 'Segoe UI', Arial, sans-serif;
  background: linear-gradient(135deg, #eef2ff, #f8fafc);
  min-height: 100vh;
}

.container {
  max-width: 1250px;
  margin: auto;
  background: rgba(255, 255, 255, 0.92);
  padding: 30px;
  border-radius: 18px;
  box-shadow: 0 12px 35px rgba(15, 23, 42, 0.12);
  backdrop-filter: blur(8px);
}

h1 {
  margin: 0 0 25px;
  font-size: 32px;
  font-weight: 700;
  color: #111827;
  text-align: center;
  letter-spacing: 0.5px;
}

h2 {
  margin: 25px 0 14px;
  font-size: 20px;
  font-weight: 600;
  color: #374151;
}

.form-box {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  align-items: center;
}

input {
  flex: 1;
  min-width: 220px;
  padding: 12px 14px;
  border: 1px solid #dbe2ea;
  border-radius: 10px;
  background: #ffffff;
  font-size: 14px;
  color: #111827;
  transition: all 0.25s ease;
}

input::placeholder {
  color: #9ca3af;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 4px rgba(37, 99, 235, 0.12);
  transform: translateY(-1px);
}

button {
  border: none;
  border-radius: 10px;
  padding: 12px 18px;
  min-width: 95px;
  font-size: 14px;
  font-weight: 600;
  color: white;
  cursor: pointer;
  transition: all 0.25s ease;
  display: inline-flex;
  align-items: center;
  justify-content: center;
}

button:hover {
  transform: translateY(-2px);
}

button:active {
  transform: scale(0.98);
}

.form-box button {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  box-shadow: 0 8px 18px rgba(37, 99, 235, 0.22);
}

.edit-btn {
  background: linear-gradient(135deg, #f59e0b, #d97706);
  margin-right: 6px;
}

.delete-btn {
  background: linear-gradient(135deg, #ef4444, #dc2626);
}

table {
  width: 100%;
  margin-top: 18px;
  border-collapse: collapse;
  overflow: hidden;
  border-radius: 14px;
  background: #ffffff;
  box-shadow: 0 8px 24px rgba(15, 23, 42, 0.08);
}

th {
  background: linear-gradient(135deg, #111827, #1f2937);
  color: white;
  font-size: 14px;
  font-weight: 600;
  padding: 14px;
  text-align: left;
}

td {
  padding: 14px;
  color: #374151;
  border-bottom: 1px solid #eef2f7;
}

tr:last-child td {
  border-bottom: none;
}

tr:hover td {
  background: #f8fafc;
}

p {
  margin-top: 14px;
  padding: 14px;
  border-radius: 10px;
  background: #f9fafb;
  color: #6b7280;
  text-align: center;
  font-weight: 500;
}

@media (max-width: 768px) {
  body {
    padding: 15px;
  }

  .container {
    padding: 20px;
  }

  h1 {
    font-size: 26px;
  }

  .form-box {
    flex-direction: column;
    align-items: stretch;
  }

  input,
  .form-box button {
    width: 100%;
  }

  table {
    font-size: 13px;
  }

  th,
  td {
    padding: 10px;
  }
}
