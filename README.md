import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";
import "./ChatScreen.css"

export function ChatScreen() {
    const [messages, setMessages] = useState([]);
    const [userInput, setUserInput] = useState("");
    const [isOpen, setIsOpen] = useState(false);

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

    const toggleSidebar = () => {
        setIsOpen(!isOpen);
    };

    return (
        <>
            <button className="toggle-button" onClick={toggleSidebar}>
                Chat
            </button>
            <div className={`upload-container ${isOpen ? 'open' : ''}`}>
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
                        <button onClick={handleSend}><FontAwesomeIcon icon={faPaperPlane} /></button>
                    </div>
                </div>
            </div>
        </>
    );
}


/* ChatScreen.css */

.upload-container {
  position: fixed;
  top: 0;
  right: -300px;
  height: 100%;
  width: 300px;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 10px 0 0 10px;
  transition: right 0.5s ease;
  display: flex;
  flex-direction: column;
}

.upload-container.open {
  right: 0;
}

.upload-container h3 {
  text-align: center;
  color: #fff;
}

h3 {
  text-align: center;
  margin: 10px 0;
  color: #fff;
}

.chat-messages {
  flex: 1;
  max-height: calc(100% - 120px);
  padding: 10px;
  margin: 10px 10px;
  border-radius: 5px;
  overflow-y: auto;
  background-color: #f9f9f9;
}

.chat-message {
  padding: 10px;
  margin: 5px 0;
  border-radius: 4px;
  opacity: 0;
  animation: fadeIn 0.5s forwards;
}

@keyframes fadeIn {
  to {
    opacity: 1;
  }
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
  margin: 10px;
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
  transition: background-color 0.3s ease-in-out;
}

.chat-input button:hover {
  background-color: #0056b3;
}

.toggle-button {
  position: fixed;
  top: 20px;
  right: 20px;
  padding: 10px 20px;
  border: none;
  border-radius: 24px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  cursor: pointer;
  transition: background-color 0
