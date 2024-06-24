import React, { useState, useEffect } from "react";
import Select from "react-select";
import "./Insights.css";

export function Insights({ selectedQuestion }) {
  const [localities] = useState([
    { value: "England", label: "England" },
    { value: "Los Angeles", label: "Los Angeles" },
    { value: "Chicago", label: "Chicago" },
    { value: "Houston", label: "Houston" },
    { value: "Phoenix", label: "Phoenix" }
  ]);
  const [selectedLocality, setSelectedLocality] = useState(null);
  const [questionInfo, setQuestionInfo] = useState(null);

  // Simulated data for question info
  const questionData = {
    "School Transfers": "Information about School Transfers...",
    "School Placements": "How to appeal a school placement decision.",
    "Teaching Methodology": "Information about Teaching Methodology...",
    "SEN/Disability": "Information about SEN/Disability...",
    "Enrichment & Extra Curr.": "Information about Enrichment & Extra Curricular...",
    "Transportation": "Information about Transportation..."
  };

  useEffect(() => {
    // Update question info when selected question changes
    if (selectedQuestion) {
      setQuestionInfo(questionData[selectedQuestion]);
    } else {
      setQuestionInfo(null);
    }
  }, [selectedQuestion]);

  const handleLocalityChange = (selectedOption) => {
    setSelectedLocality(selectedOption);
  };

  return (
    <div className="insights-container">
      <h3>Insights</h3>
      <div className="locality-section">
        <h4>Choose Your Locality</h4>
        <Select
          className="dropdown"
          value={selectedLocality}
          onChange={handleLocalityChange}
          options={localities}
          placeholder="Select a locality"
          isClearable
        />
        {selectedLocality && <div className="selected-message">You selected: {selectedLocality.label}</div>}
      </div>
      {questionInfo && (
        <div className="selected-question">
          <h4>{selectedQuestion}</h4>
          <p>{questionInfo}</p>
        </div>
      )}
    </div>
  );
}





import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane, faBars, faTimes } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

export function Chat({ onQuestionClick }) {
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
  );
}





import React, { useState, useEffect } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faPaperPlane, faBars, faTimes } from "@fortawesome/free-solid-svg-icons";
import "./Chat.css";

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
  );
}
