import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane, faBars, faTimes } from "@fortawesome/free-solid-svg-icons";
import "./ChatScreen.css";

export function ChatScreen() {
  const [messages, setMessages] = useState([]);
  const [userInput, setUserInput] = useState("");
  const [isChatOpen, setIsChatOpen] = useState(false);

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

  const toggleChat = () => {
    setIsChatOpen(!isChatOpen);
  };

  return (
    <div className="chat-screen">
      <div className="hamburger-menu" onClick={toggleChat}>
        <FontAwesomeIcon icon={isChatOpen ? faTimes : faBars} />
      </div>
      <div className={`chat-content ${isChatOpen ? "open" : ""}`}>
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








.chat-screen {
  position: relative;
}

.hamburger-menu {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 1.5rem;
  cursor: pointer;
  z-index: 1000;
  color: #fff;
}

.chat-content {
  position: fixed;
  top: 0;
  left: -100%;
  width: 350px; /* Adjust width as needed */
  height: 100%;
  background-color: #fff;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.2);
  transition: left 0.5s cubic-bezier(0.77, 0, 0.175, 1);
  z-index: 999;
  display: flex;
  flex-direction: column;
  padding-top: 50px; /* Adjust based on header height */
}

.chat-content.open {
  left: 0;
}

.chat-messages {
  padding: 20px;
  overflow-y: auto;
  flex-grow: 1;
  background: #f9f9f9;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

.chat-input {
  display: flex;
  padding: 10px;
  background: #fff;
  border-top: 1px solid #eee;
}

.chat-input input {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
  outline: none;
  transition: border-color 0.3s;
}

.chat-input input:focus {
  border-color: #007bff;
}

.chat-input button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.5rem;
  margin-left: 10px;
  color: #007bff;
  outline: none;
  transition: color 0.3s;
}

.chat-input button:hover {
  color: #0056b3;
}

.chat-message {
  margin-bottom: 10px;
  padding: 10px;
  border-radius: 10px;
  max-width: 80%;
  word-wrap: break-word;
  animation: fadeIn 0.3s ease-in-out;
}

.chat-message.user {
  background-color: #e0f7fa;
  align-self: flex-end;
  border-bottom-right-radius: 0;
}

.chat-message.bot {
  background-color: #f1f1f1;
  align-self: flex-start;
  border-bottom-left-radius: 0;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
