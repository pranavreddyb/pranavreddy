/* employee-list.css - Premium UI */

body{
  margin:0;
  padding:0;
  font-family: 'Segoe UI', Arial, sans-serif;
  background:linear-gradient(135deg,#eef2ff,#f8fafc);
}

.container{
  max-width:1300px;
  margin:40px auto;
  background:#ffffff;
  padding:32px;
  border-radius:20px;
  box-shadow:0 12px 35px rgba(0,0,0,0.08);
}

h1{
  margin:0 0 24px;
  font-size:44px;
  color:#ef4444;
  font-weight:700;
}

h3{
  margin:22px 0 14px;
  color:#111827;
  font-size:24px;
}

.form-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
  gap:14px;
  margin-bottom:26px;
  align-items:center;
}

input{
  width:100%;
  padding:13px 14px;
  border:1px solid #dbe2ea;
  border-radius:12px;
  font-size:15px;
  background:#f9fafb;
  outline:none;
  box-sizing:border-box;
  transition:0.25s ease;
}

input:focus{
  border-color:#2563eb;
  background:#fff;
  box-shadow:0 0 0 4px rgba(37,99,235,0.12);
}

button{
  border:none;
  border-radius:12px;
  padding:12px 18px;
  font-weight:600;
  cursor:pointer;
  transition:0.2s ease;
}

button:hover{
  transform:translateY(-1px);
  opacity:0.95;
}

.add-btn{
  background:linear-gradient(135deg,#2563eb,#1d4ed8);
  color:#fff;
}

.view-btn{
  background:#10b981;
  color:#fff;
  margin-right:6px;
}

.edit-btn{
  background:#f59e0b;
  color:#fff;
  margin-right:6px;
}

.delete-btn{
  background:#ef4444;
  color:#fff;
}

.employee-table{
  width:100%;
  border-collapse:separate;
  border-spacing:0;
  overflow:hidden;
  border-radius:16px;
  box-shadow:0 10px 24px rgba(0,0,0,0.06);
}

.employee-table th{
  background:linear-gradient(135deg,#111827,#1f2937);
  color:#fff;
  padding:15px;
  text-align:left;
  font-size:15px;
}

.employee-table td{
  padding:15px;
  border-bottom:1px solid #eef2f7;
  background:#fff;
}

.employee-table tr:nth-child(even) td{
  background:#f9fafb;
}

.employee-table tr:hover td{
  background:#eef6ff;
}

p{
  margin-top:18px;
  color:#6b7280;
  font-size:15px;
}

@media (max-width:768px){
  .container{
    margin:15px;
    padding:18px;
  }

  h1{
    font-size:34px;
  }

  h3{
    font-size:20px;
  }

  .employee-table{
    display:block;
    overflow-x:auto;
    white-space:nowrap;
  }

  .view-btn,
  .edit-btn{
    margin-bottom:6px;
  }
}
