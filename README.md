.overlay{
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
  animation: fadeIn 0.25s ease;
}

.modal-box{
  width: 380px;
  background: #111827;
  color: white;
  padding: 28px;
  border-radius: 18px;
  box-shadow: 0 20px 50px rgba(0,0,0,0.35);
  text-align: center;
  animation: popIn 0.28s ease;
}

.modal-box h2{
  margin-bottom: 12px;
}

.modal-box p{
  color: #cbd5e1;
  margin-bottom: 24px;
}

.buttons{
  display:flex;
  justify-content:center;
  gap:12px;
}

button{
  border:none;
  padding:10px 18px;
  border-radius:10px;
  font-weight:600;
  cursor:pointer;
}

.cancel-btn{
  background:#374151;
  color:white;
}

.confirm-btn{
  background:#2563eb;
  color:white;
}

@keyframes fadeIn{
  from{
    opacity:0;
  }
  to{
    opacity:1;
  }
}

@keyframes popIn{
  from{
    opacity:0;
    transform:scale(0.85) translateY(15px);
  }
  to{
    opacity:1;
    transform:scale(1) translateY(0);
  }
}
