.chat-container {
  max-width: 900px;
  margin: 20px auto;
  padding: 16px;
}

.messages {
  min-height: 400px;
  max-height: 500px;
  overflow-y: auto;
  margin-bottom: 16px;
}

.message {
  padding: 10px 14px;
  margin: 8px 0;
  border-radius: 8px;
}

.message.user {
  background: #e3f2fd;
  text-align: right;
}

.message.ai {
  background: #f5f5f5;
}

.input-area {
  display: flex;
  gap: 12px;
  align-items: flex-end;
}

.input-field {
  flex: 1;
}

.loading {
  display: flex;
  justify-content: center;
  margin: 16px 0;
}
