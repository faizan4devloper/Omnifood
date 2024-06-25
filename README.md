import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";
import "./ChatScreen.css";

export function ChatScreen() {
  const [messages, setMessages] = useState([]);
  const [userInput, setUserInput] = useState("");

  const handleSend = () => {
    if (userInput.trim()) {
      const newMessage = { sender: "user", text: userInput };
      setMessages([...messages, newMessage]);
      setUserInput("");

      // Simulate bot response
      setTimeout(() => {
        const botMessage = { sender: "bot", text: "This is a bot response." };
        setMessages(prevMessages => [...prevMessages, botMessage]);
      }, 1000);
    }
  };

  return (
    <div className="upload-container">
      <div className="chat-content">
        <h3>Live Conversation</h3>
        <div className="chat-messages">
          {messages.map((message, index) => (
            <div key={index} className={`chat-message ${message.sender}`}>
              {message.text}
            </div>
          ))}
        </div>
        <div className="chat-input">
          <input
            type="text"
            value={userInput}
            onChange={(e) => setUserInput(e.target.value)}
            onKeyPress={(e) => e.key === "Enter" && handleSend()}
            placeholder="Type a message..."
          />
          <button onClick={handleSend}>
            <FontAwesomeIcon icon={faPaperPlane} />
          </button>
        </div>
      </div>
    </div>
  );
}









.upload-container {
  background-color: rgba(0, 0, 0, 0.75);
  margin: 80px auto;
  border-radius: 10px;
  width: 400px;
  padding: 20px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.upload-container h3 {
  text-align: center;
  color: #fff;
  margin-bottom: 20px;
}

.chat-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.chat-messages {
  flex: 1;
  width: 100%;
  max-height: 300px;
  padding: 10px;
  margin: 10px 0;
  border-radius: 5px;
  overflow-y: auto;
  background-color: #f1f1f1;
  box-shadow: inset 0 4px 8px rgba(0, 0, 0, 0.1);
}

.chat-message {
  padding: 10px;
  margin: 5px 0;
  border-radius: 4px;
  animation: fadeIn 0.5s forwards;
}

@keyframes fadeIn {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.chat-message.user {
  background-color: #d1e7dd;
  text-align: right;
  border-bottom-right-radius: 0;
  align-self: flex-end;
}

.chat-message.bot {
  background-color: #f8d7da;
  text-align: left;
  border-bottom-left-radius: 0;
  align-self: flex-start;
}

.chat-input {
  display: flex;
  width: 100%;
  padding: 10px;
  margin-top: 10px;
  border-radius: 5px;
  border-top: 1px solid #ccc;
  background-color: #fff;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.chat-input input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
  transition: border-color 0.3s;
}

.chat-input input:focus {
  border-color: #6f36cd;
}

.chat-input button {
  padding: 10px 20px;
  border: none;
  border-radius: 24px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s ease-in-out;
}

.chat-input button:hover {
  background-color: #0056b3;
}

.chat-input button:active {
  transform: scale(0.95);
}
