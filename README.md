*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

:host{
  display:block;
  min-height:100vh;
  padding:40px;
  font-family:Inter, Arial, sans-serif;
  background:linear-gradient(135deg,#eef2ff,#f8fafc,#e0f2fe);
}

.container{
  max-width:1320px;
  margin:auto;
  background:#ffffff;
  border-radius:28px;
  padding:32px;
  box-shadow:0 25px 60px rgba(15,23,42,0.12);
}

h1{
  font-size:44px;
  font-weight:800;
  color:#0f172a;
  margin-bottom:24px;
  letter-spacing:-1px;
}

h3{
  font-size:24px;
  color:#1e293b;
  margin:18px 0 14px;
}

.form-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(190px,1fr));
  gap:14px;
  margin-bottom:28px;
}

input{
  padding:14px 16px;
  border:1px solid #dbe2ea;
  border-radius:14px;
  background:#f8fafc;
  font-size:14px;
  outline:none;
}

input:focus{
  border-color:#2563eb;
  background:#fff;
  box-shadow:0 0 0 4px rgba(37,99,235,0.12);
}

button{
  border:none;
  border-radius:14px;
  padding:12px 18px;
  font-weight:700;
  cursor:pointer;
  transition:0.2s;
}

button:hover{
  transform:translateY(-2px);
}

.add-btn{
  background:linear-gradient(135deg,#2563eb,#1d4ed8);
  color:#fff;
  box-shadow:0 10px 22px rgba(37,99,235,0.25);
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
  border-collapse:separate;
  border-spacing:0;
  overflow:hidden;
  border-radius:18px;
  background:#fff;
  box-shadow:0 10px 30px rgba(15,23,42,0.08);
}

.employee-table th{
  background:#0f172a;
  color:#fff;
  padding:16px;
  text-align:left;
}

.employee-table td{
  padding:16px;
  border-top:1px solid #eef2f7;
  color:#334155;
}

.employee-table tr:hover td{
  background:#f8fafc;
}

@media(max-width:768px){
  :host{padding:16px;}
  .container{padding:18px;}
  h1{font-size:32px;}
}
