/* employee-list.css */

body{
  margin:0;
  padding:0;
  font-family: Arial, sans-serif;
  background:#f8fafc;
}

.container{
  padding:30px;
  max-width:1400px;
  margin:auto;
}

h1{
  color:#ef4444;
  margin-bottom:20px;
  font-size:42px;
}

h3{
  margin:20px 0 15px;
  color:#111827;
}

.form-row{
  display:flex;
  flex-wrap:wrap;
  gap:12px;
  margin-bottom:25px;
}

input{
  padding:12px 14px;
  border:1px solid #d1d5db;
  border-radius:10px;
  width:220px;
  outline:none;
  font-size:15px;
  transition:0.3s;
}

input:focus{
  border-color:#2563eb;
  box-shadow:0 0 0 3px rgba(37,99,235,0.15);
}

button{
  border:none;
  padding:11px 16px;
  border-radius:10px;
  cursor:pointer;
  font-weight:600;
  transition:0.3s;
}

button:hover{
  transform:translateY(-1px);
  opacity:0.92;
}

.add-btn{
  background:#2563eb;
  color:white;
}

.view-btn{
  background:#10b981;
  color:white;
  margin-right:6px;
}

.edit-btn{
  background:#f59e0b;
  color:white;
  margin-right:6px;
}

.delete-btn{
  background:#ef4444;
  color:white;
}

.employee-table{
  width:100%;
  border-collapse:collapse;
  margin-top:15px;
  background:white;
  border-radius:14px;
  overflow:hidden;
  box-shadow:0 8px 20px rgba(0,0,0,0.08);
}

.employee-table th,
.employee-table td{
  padding:14px;
  border-bottom:1px solid #e5e7eb;
  text-align:left;
}

.employee-table th{
  background:#111827;
  color:white;
}

.employee-table tr:hover{
  background:#f9fafb;
}

p{
  margin-top:18px;
  color:#6b7280;
}

@media (max-width:768px){
  .container{
    padding:15px;
  }

  h1{
    font-size:32px;
  }

  input{
    width:100%;
  }

  .form-row{
    flex-direction:column;
  }

  .employee-table{
    display:block;
    overflow-x:auto;
    white-space:nowrap;
  }
