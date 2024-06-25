.upload-container{
  background-color: rgba(0, 0, 0, 0.5);
  margin:80px 0 0 10px;
  border-radius: 10px;
    width:300px;
}

.upload-container h3{
    text-align: center;
    color:#fff;
}

h3 {
    text-align: center;
    margin: 10px 0;
    color: #fff;
}

.chat-content{
  display: column;
  align-items: center;
  justify-content: center;
}
.chat-messages {
    flex: 1;
    /*height: 250px;*/
    max-height: 250px;
    padding: 10px;
    margin: 60px 20px;
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
    margin: 20px;
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





import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";
import "./ChatScreen.css"

export function ChatScreen(){
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
    

    
    return <div className="upload-container">
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
}
