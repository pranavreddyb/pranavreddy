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
  padding: 36px;
  border-radius: 22px;
  box-shadow: 0 24px 55px rgba(0,0,0,0.22);
}

h1 {
  margin: 0 0 30px;
  text-align: center;
  font-size: 36px;
  font-weight: 800;
  color: #111827;
  letter-spacing: 0.4px;
}

h2 {
  margin: 28px 0 16px;
  font-size: 22px;
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
  height: 50px;
  border-radius: 12px;
  font-size: 14px;
  box-sizing: border-box;
}

input {
  width: 100%;
  padding: 0 15px;
  border: 1px solid #94a3b8;
  background: #ffffff;
  color: #111827;
  font-weight: 500;
  box-shadow: 0 1px 2px rgba(0,0,0,0.05);
}

input::placeholder {
  color: #334155;
  font-weight: 600;
}

input:focus {
  outline: none;
  border-color: #2563eb;
  box-shadow: 0 0 0 4px rgba(37,99,235,0.14);
}

button {
  border: none;
  font-weight: 700;
  color: white;
  cursor: pointer;
  transition: all 0.2s ease;
}

button:hover {
  transform: translateY(-2px);
  filter: brightness(1.03);
}

.form-box button {
  width: 140px;
  justify-self: start;
  background: #2563eb;
}

.edit-btn {
  background: #f59e0b;
  min-width: 92px;
  margin-right: 8px;
}

.delete-btn {
  background: #ef4444;
  min-width: 92px;
}

table {
  width: 100%;
  margin-top: 24px;
  border-collapse: collapse;
  overflow: hidden;
  border-radius: 14px;
}

th {
  background: #111827;
  color: #ffffff;
  padding: 16px;
  text-align: left;
  font-size: 14px;
  font-weight: 800;
}

td {
  padding: 18px 16px;
  border-bottom: 1px solid #e5e7eb;
  color: #111827;
  font-weight: 600;
}

tr {
  transition: background 0.2s ease;
}

tr:hover {
  background: #f8fafc;
}

p {
  margin-top: 18px;
  padding: 15px;
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
    font-size: 30px;
  }

  h2 {
    font-size: 20px;
  }
}
