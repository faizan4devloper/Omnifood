import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";

import "./Chat.css";

export function Chat() {
    const [messages, setMessages] = useState([]);
    const [userInput, setUserInput] = useState("");
    const [mostAskedQuestions, setMostAskedQuestions] = useState([
        "What is your return policy?",
        "How do I track my order?",
        "Can I purchase items again?",
    ]);

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

    const handleQuestionClick = (question) => {
        setUserInput(question);
        handleSend();
    };

    return (
        <div className="chat-container">
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
            <div className="most-asked-questions">
                <h4>Most Asked Questions</h4>
                <ul>
                    {mostAskedQuestions.map((question, index) => (
                        <li key={index} onClick={() => handleQuestionClick(question)}>
                            {question}
                        </li>
                    ))}
                </ul>
            </div>
        </div>
    );
}





.chat-container {
    background-color: rgba(0, 0, 0, 0.5);
    margin: 80px 0 0 10px;
    border-radius: 10px;
    width: 400px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    height: 600px; /* Increased height to accommodate questions */
}

h3, h4 {
    text-align: center;
    margin: 10px 0;
    color: #fff;
}

.chat-messages {
    flex: 1;
    padding: 10px;
    margin: 20px;
    border-radius: 5px;
    overflow-y: auto;
    background-color: #f9f9f9;
}

.chat-message {
    padding: 10px;
    margin: 5px 0;
    border-radius: 4px;
    transition: background-color 0.3s ease-in-out;
}

.chat-message.user {
    background-color: #d1e7dd;
    text-align: right;
}

.chat-message.bot {
    background-color: #f8d7da;
    text-align: left;
}

.chat-message:hover {
    background-color: #e9ecef;
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
    transition: border-color 0.3s ease-in-out;
}

.chat-input input:focus {
    border-color: #1f77f6;
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

.most-asked-questions {
    padding: 10px;
    margin: 20px;
    border-radius: 5px;
    background-color: #fff;
}

.most-asked-questions h4 {
    color: #333;
}

.most-asked-questions ul {
    list-style: none;
    padding: 0;
}

.most-asked-questions li {
    padding: 10px;
    margin: 5px 0;
    background-color: #e9ecef;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
}

.most-asked-questions li:hover {
    background-color: #ccc;
}
