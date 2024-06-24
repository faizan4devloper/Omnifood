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
  const [selectedQuestion, setSelectedQuestion] = useState();

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

  const handleSendQuestionInfo = (questionInfo) => {
    // Implement the logic to send question info to the Chat component
    // For now, you can log it to the console
    console.log("Question info sent to Chat:", questionInfo);
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
          <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
        </div>
      )}
    </div>
  );
}

export default App;




import React, { useState, useEffect } from "react";
import './App.css';
import { UploadedDoc } from "./components/UploadedDoc";
import { Chat } from "./components/Chat";
import { Insights } from "./components/Insights";
import { Login } from "./components/Login";
import { Landing } from "./components/Landing";
import Modal from 'react-modal';

function App() {
  const [view, setView] = useState('login'); // 'login', 'landing', 'main'
  const [advisorType, setAdvisorType] = useState('');
  const [selectedQuestion, setSelectedQuestion] = useState();
  const [isModalOpen, setIsModalOpen] = useState(true);

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

  const handleSendQuestionInfo = (questionInfo) => {
    // Implement the logic to send question info to the Chat component
    // For now, you can log it to the console
    console.log("Question info sent to Chat:", questionInfo);
  };

  useEffect(() => {
    // Set a timeout to close the modal after 3 seconds
    const timeout = setTimeout(() => {
      setIsModalOpen(false);
    }, 3000);

    // Clear the timeout when the component unmounts
    return () => clearTimeout(timeout);
  }, []);

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
          <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
        </div>
      )}
      <Modal isOpen={isModalOpen}>
        <h2>Hello, this is a modal!</h2>
        <p>This modal will automatically close after 3 seconds.</p>
      </Modal>
    </div>
  );
}

export default App;
