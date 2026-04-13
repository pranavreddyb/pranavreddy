app.css

body {
  margin: 0;
  padding: 45px 20px;
  font-family: 'Segoe UI', Arial, sans-serif;
  min-height: 100vh;
  background:
    radial-gradient(circle at 0% 0%, rgba(59,130,246,0.20), transparent 28%),
    radial-gradient(circle at 100% 100%, rgba(168,85,247,0.18), transparent 30%),
    radial-gradient(circle at 50% 20%, rgba(14,165,233,0.12), transparent 25%),
    linear-gradient(135deg, #eef2ff, #f8fafc, #ffffff);
}

.container {
  max-width: 1350px;
  margin: auto;
  padding: 36px;
  border-radius: 30px;
  background: rgba(255,255,255,0.78);
  backdrop-filter: blur(22px);
  border: 1px solid rgba(255,255,255,0.55);
  box-shadow:
    0 30px 60px rgba(15,23,42,0.14),
    0 14px 28px rgba(15,23,42,0.08);
  position: relative;
  overflow: hidden;
}

.container::before {
  content: "";
  position: absolute;
  inset: 0;
  background: linear-gradient(120deg, rgba(255,255,255,0.22), transparent 35%, rgba(255,255,255,0.08));
  pointer-events: none;
}

h1 {
  margin: 0 0 30px;
  text-align: center;
  font-size: 40px;
  font-weight: 800;
  color: #0f172a;
  letter-spacing: 0.8px;
  position: relative;
}

h1::after {
  content: "";
  display: block;
  width: 90px;
  height: 4px;
  margin: 12px auto 0;
  border-radius: 10px;
  background: linear-gradient(135deg, #2563eb, #7c3aed);
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
  align-items: center;
  padding: 20px;
  border-radius: 20px;
  background: rgba(255,255,255,0.72);
  box-shadow:
    inset 0 1px 0 rgba(255,255,255,0.75),
    0 10px 24px rgba(15,23,42,0.05);
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
  transform: translateY(-2px);
}

button {
  border: none;
  border-radius: 14px;
  padding: 14px 22px;
  min-width: 120px;
  font-size: 14px;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: all 0.25s ease;
}

button:hover {
  transform: translateY(-3px);
  filter: brightness(1.04);
}

button:active {
  transform: scale(0.98);
}

.form-box button {
  background: linear-gradient(135deg, #2563eb, #1d4ed8, #1e40af);
  box-shadow: 0 14px 24px rgba(37,99,235,0.28);
}

.edit-btn {
  background: linear-gradient(135deg, #f59e0b, #f97316);
  box-shadow: 0 10px 18px rgba(245,158,11,0.24);
  margin-right: 8px;
}

.delete-btn {
  background: linear-gradient(135deg, #ef4444, #dc2626);
  box-shadow: 0 10px 18px rgba(239,68,68,0.24);
}

table {
  width: 100%;
  margin-top: 22px;
  border-collapse: separate;
  border-spacing: 0;
  overflow: hidden;
  border-radius: 22px;
  background: rgba(255,255,255,0.95);
  box-shadow:
    0 18px 38px rgba(15,23,42,0.09),
    0 8px 18px rgba(15,23,42,0.05);
}

th {
  background: linear-gradient(135deg, #0f172a, #1e293b, #334155);
  color: white;
  padding: 17px;
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

tr:nth-child(even) td {
  background: rgba(248,250,252,0.65);
}

tr:hover td {
  background: linear-gradient(135deg, #f8fafc, #eef2ff);
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
    border-radius: 22px;
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
