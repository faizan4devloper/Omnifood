import React, { useState } from "react";
import './App.css';
import { UploadedDoc } from "./components/UploadedDoc";
import { Chat } from "./components/Chat";
import { Insights } from "./components/Insights";
import { Login } from "./components/Login";
import { Landing } from "./components/Landing";

function App() {
  const [view, setView] = useState('login'); // 'login', 'landing', 'main'
  const [advisorType, setAdvisorType] = useState('');
  const [selectedQuestion, setSelectedQuestion] = useState(null);

  const handleLogin = () => {
    setView('landing');
  };

  const handleEnterMain = (type) => {
    setAdvisorType(type);
    setView('main');
  };

  const handleGoBack = () => {
    if (view === 'landing') {
      setView('login');
    } else if (view === 'main') {
      setView('landing');
    }
  };

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  return (
    <div className="app">
      <nav className="breadcrumbs">
        <ul>
          <li>
            <a href="#" onClick={handleGoBack}>
              Login
            </a>
          </li>
          {view === 'main' && (
            <>
              <li>
                <a href="#">
                  {advisorType} Advisor
                </a>
              </li>
            </>
          )}
          {view === 'landing' && (
            <li>
              <a>Landing</a>
            </li>
          )}
        </ul>
      </nav>
      {view === 'login' && <Login onLogin={handleLogin} />}
      {view === 'landing' && <Landing onEnterMain={handleEnterMain} />}
      {view === 'main' && (
        <div className="main-container">
          <h2 className="advisor-heading">{advisorType} Advisor</h2>
          <UploadedDoc />
          <Chat onQuestionClick={handleQuestionClick} />
          <Insights selectedQuestion={selectedQuestion} />
        </div>
      )}
    </div>
  );
}

export default App;






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
import "./Insights.css";

export function Insights({ selectedQuestion }) {
  const [questionInfo, setQuestionInfo] = useState(null);

  // Simulated data for question info
  const questionData = {
    "School Transfers": "Information about School Transfers...",
    "School Placements": "Information about School Placements...",
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

  return (
    <div className="insights-container">
      <h3>Insights</h3>
      {questionInfo ? (
        <div className="question-info">
          <h4>{selectedQuestion}</h4>
          <p>{questionInfo}</p>
        </div>
      ) : (
        <p>No question selected</p>
      )}
    </div>
  );
}














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
    "School Placements": "Information about School Placements...",
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
      {selectedQuestion && (
        <div className="selected-question">
          <h4>Information about:</h4>
          <p>{selectedQuestion}</p>
        </div>
      )}
    </div>
  );
}
