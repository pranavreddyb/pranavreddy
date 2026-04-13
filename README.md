app.css

body {
  margin: 0;
  padding: 40px 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
  min-height: 100vh;
  background:
    radial-gradient(circle at top left, rgba(59,130,246,0.18), transparent 30%),
    radial-gradient(circle at bottom right, rgba(168,85,247,0.18), transparent 30%),
    linear-gradient(135deg, #eef2ff, #f8fafc, #ffffff);
}

.container {
  max-width: 1320px;
  margin: auto;
  padding: 34px;
  border-radius: 28px;
  background: rgba(255,255,255,0.72);
  backdrop-filter: blur(18px);
  border: 1px solid rgba(255,255,255,0.45);
  box-shadow:
    0 25px 55px rgba(15,23,42,0.14),
    0 10px 25px rgba(15,23,42,0.08);
}

h1 {
  margin: 0 0 30px;
  text-align: center;
  font-size: 38px;
  font-weight: 800;
  color: #0f172a;
  letter-spacing: 0.8px;
}

h2 {
  margin: 30px 0 14px;
  font-size: 22px;
  font-weight: 700;
  color: #1e293b;
}

.form-box {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  align-items: center;
  padding: 18px;
  border-radius: 18px;
  background: rgba(255,255,255,0.72);
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.7);
}

input {
  width: 100%;
  box-sizing: border-box;
  padding: 14px 16px;
  border: 1px solid #dbe2ea;
  border-radius: 14px;
  background: rgba(255,255,255,0.95);
  font-size: 14px;
  color: #111827;
  transition: all 0.25s ease;
}

input::placeholder {
  color: #94a3b8;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 5px rgba(37,99,235,0.12);
  transform: translateY(-1px);
}

button {
  border: none;
  border-radius: 14px;
  padding: 14px 20px;
  min-width: 115px;
  font-size: 14px;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: all 0.25s ease;
}

button:hover {
  transform: translateY(-3px);
}

button:active {
  transform: scale(0.98);
}

.form-box button {
  background: linear-gradient(135deg, #2563eb, #1d4ed8, #1e40af);
  box-shadow: 0 14px 24px rgba(37,99,235,0.26);
}

.edit-btn {
  background: linear-gradient(135deg, #f59e0b, #f97316);
  box-shadow: 0 10px 18px rgba(245,158,11,0.22);
  margin-right: 8px;
}

.delete-btn {
  background: linear-gradient(135deg, #ef4444, #dc2626);
  box-shadow: 0 10px 18px rgba(239,68,68,0.22);
}

table {
  width: 100%;
  margin-top: 22px;
  border-collapse: separate;
  border-spacing: 0;
  overflow: hidden;
  border-radius: 20px;
  background: rgba(255,255,255,0.92);
  box-shadow:
    0 18px 35px rgba(15,23,42,0.08),
    0 8px 18px rgba(15,23,42,0.05);
}

th {
  background: linear-gradient(135deg, #0f172a, #1e293b, #334155);
  color: white;
  padding: 16px;
  text-align: left;
  font-size: 14px;
  font-weight: 700;
}

td {
  padding: 16px;
  font-size: 14px;
  color: #334155;
  border-bottom: 1px solid #eef2f7;
}

tr:last-child td {
  border-bottom: none;
}

tr:hover td {
  background: linear-gradient(135deg, #f8fafc, #f1f5f9);
}

p {
  margin-top: 18px;
  padding: 18px;
  border-radius: 16px;
  background: linear-gradient(135deg, #f8fafc, #f1f5f9);
  color: #64748b;
  text-align: center;
  font-weight: 600;
}

@media (max-width: 768px) {
  body {
    padding: 18px 12px;
  }

  .container {
    padding: 22px;
    border-radius: 20px;
  }

  h1 {
    font-size: 30px;
  }

  h2 {
    font-size: 20px;
  }

  th, td {
    padding: 11px;
    font-size: 13px;
  }

  button {
    width: 100%;
  }
}
