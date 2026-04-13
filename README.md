app.css

body {
  margin: 0;
  padding: 40px 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
  background:
    radial-gradient(circle at top left, #dbeafe, transparent 35%),
    radial-gradient(circle at bottom right, #e9d5ff, transparent 35%),
    linear-gradient(135deg, #eef2ff, #f8fafc);
  min-height: 100vh;
}

.container {
  max-width: 1280px;
  margin: auto;
  background: rgba(255, 255, 255, 0.88);
  backdrop-filter: blur(14px);
  border: 1px solid rgba(255,255,255,0.5);
  border-radius: 24px;
  padding: 32px;
  box-shadow:
    0 20px 45px rgba(15, 23, 42, 0.12),
    0 8px 18px rgba(15, 23, 42, 0.06);
}

h1 {
  margin: 0 0 28px;
  text-align: center;
  font-size: 34px;
  font-weight: 800;
  color: #111827;
  letter-spacing: 0.6px;
}

h2 {
  margin: 28px 0 14px;
  font-size: 20px;
  font-weight: 700;
  color: #374151;
}

.form-box {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 14px;
  align-items: center;
}

input {
  width: 100%;
  padding: 13px 15px;
  border: 1px solid #dbe2ea;
  border-radius: 12px;
  background: rgba(255,255,255,0.95);
  font-size: 14px;
  color: #111827;
  box-sizing: border-box;
  transition: all 0.25s ease;
}

input::placeholder {
  color: #9ca3af;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 4px rgba(37,99,235,0.12);
  transform: translateY(-1px);
}

button {
  border: none;
  border-radius: 12px;
  padding: 13px 18px;
  min-width: 110px;
  font-size: 14px;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: all 0.25s ease;
}

button:hover {
  transform: translateY(-2px);
  filter: brightness(1.03);
}

button:active {
  transform: scale(0.98);
}

.form-box button {
  background: linear-gradient(135deg, #2563eb, #1d4ed8);
  box-shadow: 0 10px 20px rgba(37,99,235,0.22);
}

.edit-btn {
  background: linear-gradient(135deg, #f59e0b, #d97706);
  box-shadow: 0 8px 18px rgba(245,158,11,0.22);
  margin-right: 6px;
}

.delete-btn {
  background: linear-gradient(135deg, #ef4444, #dc2626);
  box-shadow: 0 8px 18px rgba(239,68,68,0.20);
}

table {
  width: 100%;
  margin-top: 20px;
  border-collapse: separate;
  border-spacing: 0;
  overflow: hidden;
  border-radius: 18px;
  background: rgba(255,255,255,0.95);
  box-shadow:
    0 16px 30px rgba(15,23,42,0.08),
    0 6px 14px rgba(15,23,42,0.05);
}

th {
  background: linear-gradient(135deg, #111827, #1f2937);
  color: white;
  padding: 15px;
  font-size: 14px;
  font-weight: 700;
  text-align: left;
}

td {
  padding: 15px;
  color: #374151;
  border-bottom: 1px solid #eef2f7;
  font-size: 14px;
}

tr:last-child td {
  border-bottom: none;
}

tr:hover td {
  background: #f8fafc;
}

p {
  margin-top: 16px;
  padding: 16px;
  border-radius: 14px;
  background: linear-gradient(135deg, #f9fafb, #f3f4f6);
  color: #6b7280;
  text-align: center;
  font-weight: 600;
}

@media (max-width: 768px) {
  body {
    padding: 18px 12px;
  }

  .container {
    padding: 22px;
    border-radius: 18px;
  }

  h1 {
    font-size: 28px;
  }

  table {
    font-size: 13px;
  }

  th, td {
    padding: 10px;
  }
}
