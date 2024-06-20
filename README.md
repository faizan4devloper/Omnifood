import React, { useState } from "react";
import "./Chat.css";

export function Chat() {
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
        <div className="chat-container">
            <h3>Chat</h3>
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
                <button onClick={handleSend}>Send</button>
            </div>
        </div>
    );
}







/* Chat.css */

.chat-container {
    width: 400px;
    margin: 0 auto;
    border: 1px solid #ccc;
    border-radius: 8px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    height: 500px;
}

h3 {
    text-align: center;
    margin: 10px 0;
}

.chat-messages {
    flex: 1;
    padding: 10px;
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
    padding: 10px;
    border: none;
    border-radius: 4px;
    background-color: #007bff;
    color: #fff;
    cursor: pointer;
}

.chat-input button:hover {
    background-color: #0056b3;
}



const handleSend = () => {
    if (userInput.trim()) {
        const newMessage = { sender: "user", text: userInput };
        setMessages([...messages, newMessage]);
        setUserInput("");

        // Replace with your bot API URL
        fetch("https://your-bot-api.com/message", {
            method: "POST",
            headers: {
                "Content-Type": "application/json",
            },
            body: JSON.stringify({ message: userInput }),
        })
        .then(response => response.json())
        .then(data => {
            const botMessage = { sender: "bot", text: data.response };
            setMessages(prevMessages => [...prevMessages, botMessage]);
        })
        .catch(error => {
            console.error("Error:", error);
        });
    }
};






