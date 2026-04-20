.overlay{
  position: fixed;
  inset: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-box{
  width: 380px;
  background: #111827;
  color: white;
  padding: 28px;
  border-radius: 18px;
  box-shadow: 0 20px 50px rgba(0,0,0,0.35);
  text-align: center;
}

.modal-box h2{
  margin-bottom: 12px;
  font-size: 24px;
}

.modal-box p{
  color: #cbd5e1;
  margin-bottom: 24px;
  line-height: 1.5;
}

.buttons{
  display: flex;
  justify-content: center;
  gap: 12px;
}

button{
  border: none;
  padding: 10px 18px;
  border-radius: 10px;
  font-weight: 600;
  cursor: pointer;
}

.cancel-btn{
  background: #374151;
  color: white;
}

.confirm-btn{
  background: #2563eb;
  color: white;
}
