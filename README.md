*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

:host{
  display:block;
  min-height:100vh;
  padding:36px;
  font-family:Inter, Arial, sans-serif;
  background:
    radial-gradient(circle at top left, #dbeafe 0%, transparent 30%),
    radial-gradient(circle at bottom right, #ede9fe 0%, transparent 30%),
    linear-gradient(135deg, #f8fafc, #eef2ff);
}

.container{
  max-width:1320px;
  margin:auto;
  background:rgba(255,255,255,0.92);
  backdrop-filter:blur(12px);
  border:1px solid rgba(255,255,255,0.6);
  border-radius:28px;
  padding:32px;
  box-shadow:
    0 20px 60px rgba(15,23,42,0.10),
    0 8px 24px rgba(15,23,42,0.06);
}

h1{
  font-size:42px;
  font-weight:800;
  letter-spacing:-1px;
  color:#0f172a;
  margin-bottom:24px;
}

h3{
  font-size:22px;
  color:#334155;
  margin:18px 0 14px;
  font-weight:700;
}

.form-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:14px;
  margin-bottom:28px;
}

input{
  padding:14px 16px;
  border:1px solid #e2e8f0;
  border-radius:14px;
  background:#ffffff;
  font-size:14px;
  color:#0f172a;
  outline:none;
  transition:all .2s ease;
}

input::placeholder{
  color:#94a3b8;
}

input:focus{
  border-color:#2563eb;
  box-shadow:0 0 0 4px rgba(37,99,235,0.12);
  transform:translateY(-1px);
}

button{
  border:none;
  border-radius:14px;
  padding:12px 18px;
  font-size:14px;
  font-weight:700;
  cursor:pointer;
  transition:all .2s ease;
}

button:hover{
  transform:translateY(-2px);
}

button:active{
  transform:translateY(0);
}

.add-btn{
  background:linear-gradient(135deg,#2563eb,#1d4ed8);
  color:#fff;
  box-shadow:0 10px 20px rgba(37,99,235,0.22);
}

.view-btn{
  background:#ecfdf5;
  color:#059669;
  border:1px solid #a7f3d0;
}

.edit-btn{
  background:#fffbeb;
  color:#d97706;
  border:1px solid #fde68a;
}

.delete-btn{
  background:#fef2f2;
  color:#dc2626;
  border:1px solid #fecaca;
}

.employee-table{
  width:100%;
  border-collapse:separate;
  border-spacing:0;
  overflow:hidden;
  border-radius:20px;
  background:#ffffff;
  border:1px solid #e5e7eb;
  box-shadow:0 12px 30px rgba(15,23,42,0.06);
}

.employee-table th{
  background:linear-gradient(180deg,#0f172a,#1e293b);
  color:#ffffff;
  text-align:left;
  padding:16px;
  font-size:14px;
  font-weight:700;
}

.employee-table td{
  padding:16px;
  border-top:1px solid #f1f5f9;
  color:#334155;
  font-size:14px;
}

.employee-table tr:hover td{
  background:#f8fafc;
}

p{
  margin-top:14px;
  color:#64748b;
}

@media(max-width:768px){
  :host{
    padding:16px;
  }

  .container{
    padding:18px;
    border-radius:20px;
  }

  h1{
    font-size:32px;
  }

  h3{
    font-size:20px;
  }

  .employee-table{
    font-size:13px;
  }
}
