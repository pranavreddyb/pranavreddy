*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}

:host{
  display:block;
  min-height:100vh;
  font-family:Inter, Arial, sans-serif;
  background:linear-gradient(135deg,#0f172a,#111827,#1e293b);
  padding:24px;
}

.container{
  max-width:1400px;
  margin:auto;
  background:#f8fafc;
  border-radius:28px;
  overflow:hidden;
  box-shadow:0 30px 80px rgba(0,0,0,0.35);
}

/* HEADER */
.header{
  background:linear-gradient(135deg,#2563eb,#1d4ed8);
  color:white;
  padding:28px 32px;
}

.header h1{
  font-size:42px;
  font-weight:800;
  letter-spacing:-1px;
}

.header p{
  margin-top:8px;
  opacity:0.9;
  font-size:15px;
}

/* BODY */
.dashboard{
  display:grid;
  grid-template-columns:260px 1fr;
  min-height:80vh;
}

/* SIDEBAR */
.sidebar{
  background:#0f172a;
  color:#cbd5e1;
  padding:24px;
}

.sidebar h3{
  color:#fff;
  margin-bottom:20px;
  font-size:20px;
}

.menu-item{
  padding:12px 14px;
  border-radius:12px;
  margin-bottom:10px;
  background:rgba(255,255,255,0.04);
}

.menu-item.active{
  background:#2563eb;
  color:#fff;
}

/* MAIN */
.main-content{
  padding:28px;
}

/* STATS */
.stats{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
  gap:16px;
  margin-bottom:24px;
}

.stat-card{
  background:#fff;
  border-radius:18px;
  padding:20px;
  box-shadow:0 10px 24px rgba(15,23,42,0.08);
}

.stat-card span{
  color:#64748b;
  font-size:13px;
}

.stat-card h2{
  margin-top:8px;
  font-size:30px;
  color:#0f172a;
}

/* FORM */
.form-box{
  background:#fff;
  border-radius:20px;
  padding:22px;
  margin-bottom:24px;
  box-shadow:0 10px 24px rgba(15,23,42,0.06);
}

.form-box h3{
  margin-bottom:16px;
  color:#0f172a;
}

.form-row{
  display:grid;
  grid-template-columns:repeat(auto-fit,minmax(180px,1fr));
  gap:14px;
}

input{
  padding:14px;
  border:1px solid #dbe2ea;
  border-radius:12px;
  background:#f8fafc;
  outline:none;
}

input:focus{
  border-color:#2563eb;
  background:#fff;
  box-shadow:0 0 0 4px rgba(37,99,235,0.12);
}

/* BUTTONS */
button{
  border:none;
  border-radius:12px;
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

/* TABLE */
.table-box{
  background:#fff;
  border-radius:20px;
  padding:20px;
  box-shadow:0 10px 24px rgba(15,23,42,0.06);
}

.table-box h3{
  margin-bottom:16px;
  color:#0f172a;
}

.employee-table{
  width:100%;
  border-collapse:collapse;
}

.employee-table th{
  background:#0f172a;
  color:#fff;
  padding:14px;
  text-align:left;
}

.employee-table td{
  padding:14px;
  border-bottom:1px solid #eef2f7;
}

.employee-table tr:hover{
  background:#f8fafc;
}

/* MOBILE */
@media(max-width:900px){
  .dashboard{
    grid-template-columns:1fr;
  }

  .sidebar{
    display:none;
  }

  .header h1{
    font-size:32px;
  }
}
