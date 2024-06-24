import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane } from "@fortawesome/free-solid-svg-icons";
import "./ChatContent.css";

function ChatContent({ messages, userInput, setUserInput, handleSend }) {
  return (
    <div className="chat-content">
      <h3>Live Conversation</h3>
      {messages.length > 0 && (
        <div className="chat-messages">
          {messages.map((message, index) => (
            <div key={index} className={`chat-message ${message.sender}`}>
              {message.text}
            </div>
          ))}
        </div>
      )}
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
  );
}

export default ChatContent;






import React, { useState, useEffect } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faBars, faTimes } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";
import ChatContent from "./ChatContent";

export function Chat({ onQuestionClick, questionInfo }) {
  const [messages, setMessages] = useState([]);
  const [userInput, setUserInput] = useState("");
  const [mostAskedQuestions] = useState([
    "School Transfers",
    "School Placements",
    "Teaching Methodology",
    "SEN/Disability",
    "Enrichment & Extra Curr.",
    "Transportation"
  ]);
  const [showQuestions, setShowQuestions] = useState(false);

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
    setShowQuestions(false);
    onQuestionClick(question); // Notify parent component
  };

  useEffect(() => {
    // Update userInput when questionInfo changes
    if (questionInfo) {
      setUserInput(questionInfo);
    }
  }, [questionInfo]);

  const toggleQuestions = () => {
    setShowQuestions(!showQuestions);
  };

  return (
    <div className="chat-container">
      <div className="hamburger-menu" onClick={toggleQuestions}>
        <FontAwesomeIcon icon={showQuestions ? faTimes : faBars} />
      </div>
      <div className={`most-asked-questions ${showQuestions ? 'show' : ''}`}>
        <h4>Most Asked Questions</h4>
        <ul>
          {mostAskedQuestions.map((question, index) => (
            <li key={index} onClick={() => handleQuestionClick(question)}>
              {question}
            </li>
          ))}
        </ul>
      </div>
      <ChatContent 
        messages={messages}
        userInput={userInput}
        setUserInput={setUserInput}
        handleSend={handleSend}
      />
    </div>
  );
}







.chat-content {
  margin-top: 20px;
}

.chat-messages {
  margin-bottom: 20px;
  max-height: 300px;
  overflow-y: auto;
}

.chat-message.user {
  text-align: right;
}

.chat-message.bot {
  text-align: left;
}

.chat-input {
  display: flex;
  align-items: center;
}

.chat-input input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.chat-input button {
  margin-left: 10px;
  padding: 10px 20px;
  border: none;
  background: #007bff;
  color: white;
  border-radius: 4px;
  cursor: pointer;
}
