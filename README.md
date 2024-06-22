import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";

import "./Chat.css";

export function Chat() {
    const [messages, setMessages] = useState([]);
    const [userInput, setUserInput] = useState("");

    const faqs = [
        "What is your return policy?",
        "How do I track my order?",
        "Can I purchase items again?",
        "Do you have customer support?"
    ];

    const handleSend = (text) => {
        if (text.trim()) {
            const newMessage = { sender: "user", text: text };
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
        <div className="chat-container">
            <h3>Live Conversation</h3>
            <div className="chat-faqs">
                <h4>Most Asked Questions</h4>
                {faqs.map((faq, index) => (
                    <button key={index} className="faq-item" onClick={() => handleSend(faq)}>
                        {faq}
                    </button>
                ))}
            </div>
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
                    onKeyPress={(e) => e.key === "Enter" && handleSend(userInput)}
                    placeholder="Type a message..."
                />
                <button onClick={() => handleSend(userInput)}>
                    <FontAwesomeIcon icon={faPaperPlane} />
                </button>
            </div>
        </div>
    );
}









.chat-container {
    display: flex;
    flex-direction: column;
    height: 100%;
    max-width: 600px;
    margin: 0 auto;
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    font-family: Arial, sans-serif;
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}

.chat-faqs {
    padding: 10px;
    border-bottom: 1px solid #ccc;
    background-color: #f9f9f9;
}

.chat-faqs h4 {
    margin-bottom: 10px;
}

.faq-item {
    display: block;
    background: none;
    border: none;
    color: #007BFF;
    cursor: pointer;
    padding: 5px 0;
    text-align: left;
    width: 100%;
    transition: background-color 0.3s;
}

.faq-item:hover {
    background-color: #f1f1f1;
}

.chat-messages {
    flex: 1;
    padding: 10px;
    overflow-y: auto;
    display: flex;
    flex-direction: column;
}

.chat-message {
    padding: 8px 12px;
    border-radius: 18px;
    margin-bottom: 10px;
    max-width: 80%;
    animation: fadeIn 0.5s;
}

.chat-message.user {
    align-self: flex-end;
    background-color: #007BFF;
    color: white;
}

.chat-message.bot {
    align-self: flex-start;
    background-color: #E0E0E0;
    color: black;
}

.chat-input {
    display: flex;
    padding: 10px;
    border-top: 1px solid #ccc;
}

.chat-input input {
    flex: 1;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 18px;
    outline: none;
    margin-right: 10px;
    font-size: 16px;
    transition: box-shadow 0.3s;
}

.chat-input input:focus {
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
}

.chat-input button {
    background-color: #007BFF;
    border: none;
    color: white;
    padding: 10px 15px;
    border-radius: 18px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.chat-input button:hover {
    background-color: #0056b3;
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}
