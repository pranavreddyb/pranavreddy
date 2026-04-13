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
  padding: 34px;
  border-radius: 20px;
  box-shadow: 0 22px 50px rgba(0,0,0,0.22);
}

h1 {
  margin: 0 0 30px;
  text-align: center;
  font-size: 34px;
  font-weight: 800;
  color: #111827;
  letter-spacing: 0.4px;
}

h2 {
  margin: 26px 0 14px;
  font-size: 21px;
  font-weight: 800;
  color: #111827;
}

.form-box {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
  align-items: center;
}

input,
button {
  height: 48px;
  border-radius: 12px;
  font-size: 14px;
  box-sizing: border-box;
}

input {
  width: 100%;
  padding: 0 14px;
  border: 1px solid #cbd5e1;
  background: #ffffff;
  color: #111827;
  box-shadow: 0 1px 2px rgba(0,0,0,0.04);
}

input::placeholder {
  color: #475569;
  font-weight: 500;
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
  width: 140px;
  justify-self: start;
  background: #2563eb;
}

.edit-btn {
  background: #f59e0b;
  min-width: 88px;
  margin-right: 8px;
}

.delete-btn {
  background: #ef4444;
  min-width: 88px;
}

table {
  width: 100%;
  margin-top: 22px;
  border-collapse: collapse;
  overflow: hidden;
  border-radius: 14px;
}

th {
  background: #111827;
  color: #ffffff;
  padding: 14px;
  text-align: left;
  font-size: 14px;
  font-weight: 700;
}

td {
  padding: 16px 14px;
  border-bottom: 1px solid #e5e7eb;
  color: #1f2937;
  font-weight: 500;
}

tr:hover {
  background: #f8fafc;
}

p {
  margin-top: 16px;
  padding: 14px;
  border-radius: 12px;
  background: #eff6ff;
  color: #1d4ed8;
  text-align: center;
  font-weight: 700;
}

@media (max-width: 900px) {
  .form-box {
    grid-template-columns: 1fr;
  }

  .form-box button,
  .edit-btn,
  .delete-btn {
    width: 100%;
    margin-right: 0;
    margin-bottom: 8px;
  }

  .container {
    padding: 22px;
  }

  h1 {
    font-size: 28px;
  }
}
