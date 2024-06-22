.chat-container {
     background-color: rgba(0, 0, 0, 0.5);
  margin:80px 0 0 10px;
  border-radius: 10px;
    width:400px;
    border-radius: 8px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    height: 500px;
}

h3 {
    text-align: center;
    margin: 10px 0;
    color: #fff;
}

.chat-messages {
    flex: 1;
    padding: 10px;
    margin:20px;
    border-radius: 5px;
    overflow-y: auto;
    background-color: #f9f9f9;
}

.chat-message {
    padding: 10px;
    margin: 5px 0;
    border-radius: 4px;
}

.chat-message.user {
    background-color: #d1e7dd;
    text-align: right;
}

.chat-message.bot {
    background-color: #f8d7da;
    text-align: left;
}

.chat-input {
    display: flex;
    padding: 10px;
    margin:20px;
    border-radius: 5px;
    border-top: 1px solid #ccc;
    background-color: #fff;
}

.chat-input input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
}

.chat-input button {
    margin-left: 10px;
    padding: 10px 10px;
    border: none;
    border-radius: 24px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
    color: #fff;
    cursor: pointer;
}

.chat-input button:hover {
    background-color: #0056b3;
}

