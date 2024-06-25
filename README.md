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
  font-family: 'Arial', sans-serif;
}

.hamburger-menu {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 1.5rem;
  cursor: pointer;
  z-index: 1000;
  transition: transform 0.3s;
}

.hamburger-menu:hover {
  transform: scale(1.1);
}

.chat-content {
  position: fixed;
  top: 0;
  left: -100%;
  width: 350px; /* Adjust width as needed */
  height: 100%;
  background-color: #fff;
  box-shadow: 2px 0 10px rgba(0, 0, 0, 0.2);
  transition: left 0.5s ease-in-out, box-shadow 0.5s;
  z-index: 999;
}

.chat-content.open {
  left: 0;
  box-shadow: 5px 0 15px rgba(0, 0, 0, 0.3);
}

.chat-messages {
  padding: 20px;
  overflow-y: auto;
  height: calc(100% - 80px); /* Adjust height based on other content */
  background-color: #f9f9f9;
}

.chat-input {
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  padding: 10px;
  box-sizing: border-box;
  background-color: #fff;
  border-top: 1px solid #ccc;
}

.chat-input input {
  flex-grow: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
  outline: none;
  transition: box-shadow 0.3s;
}

.chat-input input:focus {
  box-shadow: 0 0 5px rgba(0, 0, 255, 0.5);
}

.chat-input button {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
  margin-left: 10px;
  color: #007bff;
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
  animation: fadeIn 0.5s ease-in-out;
}

.chat-message.user {
  background-color: #d1e7ff;
  align-self: flex-end;
  margin-left: auto;
}

.chat-message.bot {
  background-color: #e9ecef;
  align-self: flex-start;
  margin-right: auto;
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
