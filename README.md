*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

:host{
  display:block;
  min-height:100vh;
  padding:40px;
  font-family:Arial, sans-serif;
  background: linear-gradient(135deg,#0f172a,#1e293b,#334155);
}

.container{
  max-width:1200px;
  margin:auto;
  background: rgba(255,255,255,0.12);
  backdrop-filter: blur(14px);
  border:1px solid rgba(255,255,255,0.15);
  border-radius:24px;
  padding:30px;
  box-shadow:0 20px 50px rgba(0,0,0,0.25);
}

h1{
  font-size:42px;
  margin-bottom:25px;
  color:#ffffff;
  font-weight:700;
}

h3{
  color:#e2e8f0;
  margin:18px 0 14px;
  font-size:24px;
}

.form-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
  gap:14px;
  margin-bottom:25px;
}

input{
  padding:14px;
  border:none;
  border-radius:12px;
  background:rgba(255,255,255,0.9);
  font-size:15px;
  outline:none;
}

input:focus{
  box-shadow:0 0 0 3px rgba(59,130,246,0.35);
}

button{
  border:none;
  border-radius:12px;
  padding:12px 18px;
  font-weight:600;
  cursor:pointer;
  transition:0.25s;
}

button:hover{
  transform:translateY(-2px);
}

.add-btn{
  background:linear-gradient(135deg,#3b82f6,#2563eb);
  color:#fff;
}

.view-btn{
  background:#10b981;
  color:#fff;
}

.edit-btn{
  background:#f59e0b;
  color:#fff;
}

.delete-btn{
  background:#ef4444;
  color:#fff;
}

.employee-table{
  width:100%;
  border-collapse:collapse;
  overflow:hidden;
  border-radius:18px;
  background:#ffffff;
}

.employee-table th{
  background:linear-gradient(135deg,#1e293b,#0f172a);
  color:#fff;
  padding:16px;
  text-align:left;
}

.employee-table td{
  padding:16px;
  border-bottom:1px solid #e5e7eb;
}

.employee-table tr:hover{
  background:#f8fafc;
}

p{
  color:#fff;
  margin-top:15px;
}

@media(max-width:768px){
  :host{
    padding:15px;
  }

  h1{
    font-size:32px;
  }

  .container{
    padding:18px;
  }

  .employee-table{
    font-size:14px;
  }
}
