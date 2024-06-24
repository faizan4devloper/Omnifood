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







import React, { useState } from "react";
import { UploadedDoc } from "./UploadedDoc";
import { Chat } from "./Chat";
import { Insights } from "./Insights";

function MainContainer() {
  const [selectedQuestion, setSelectedQuestion] = useState(null);

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  const handleSendQuestionInfo = (questionInfo) => {
    // Implement the logic to send question info to the Chat component
    // For now, you can log it to the console
    console.log("Question info sent to Chat:", questionInfo);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">Advisor</h2>
      <UploadedDoc />
      <Chat onQuestionClick={handleQuestionClick} />
      <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
    </div>
  );
}

export default MainContainer;








import React, { useState } from "react";
import { Login } from "./components/Login";
import { Landing } from "./components/Landing";
import MainContainer from "./components/MainContainer";
import "./App.css";

function App() {
  const [view, setView] = useState("login"); // 'login', 'landing', 'main'
  const [advisorType, setAdvisorType] = useState("");

  const handleLogin = () => {
    setView("landing");
  };

  const handleEnterMain = (type) => {
    setAdvisorType(type);
    setView("main");
  };

  const handleGoBack = () => {
    if (view === "landing") {
      setView("login");
    } else if (view === "main") {
      setView("landing");
    }
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
          {view === "main" && (
            <>
              <li>
                <a href="#">{advisorType} Advisor</a>
              </li>
            </>
          )}
          {view === "landing" && (
            <li>
              <a>Landing</a>
            </li>
          )}
        </ul>
      </nav>
      {view === "login" && <Login onLogin={handleLogin} />}
      {view === "landing" && <Landing onEnterMain={handleEnterMain} />}
      {view === "main" && <MainContainer />}
    </div>
  );
}

export default App;






import React, { useState } from "react";
import { Login } from "./components/Login";
import { Landing } from "./components/Landing";
import MainContainer from "./components/MainContainer";
import "./App.css";

function App() {
  const [view, setView] = useState("login");
  const [advisorType, setAdvisorType] = useState("");

  const handleLogin = () => {
    setView("landing");
  };

  const handleEnterMain = (type) => {
    setAdvisorType(type);
    setView("main");
  };

  const handleGoBack = () => {
    if (view === "landing") {
      setView("login");
    } else if (view === "main") {
      setView("landing");
    }
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
          {view === "main" && (
            <>
              <li>
                <a href="#">{advisorType} Advisor</a>
              </li>
            </>
          )}
          {view === "landing" && (
            <li>
              <a>Landing</a>
            </li>
          )}
        </ul>
      </nav>
      {view === "login" && <Login onLogin={handleLogin} />}
      {view === "landing" && <Landing onEnterMain={handleEnterMain} />}
      {view === "main" && <MainContainer />}
    </div>
  );
}

export default App;




import React, { useState, useEffect } from "react";
import { UploadedDoc } from "./UploadedDoc";
import { Chat } from "./Chat";
import { Insights } from "./Insights";
import Modal from "./Modal";

function MainContainer() {
  const [selectedQuestion, setSelectedQuestion] = useState(null);
  const [isModalOpen, setIsModalOpen] = useState(true);

  const handleQuestionClick = (question) => {
    setSelectedQuestion(question);
  };

  const handleSendQuestionInfo = (questionInfo) => {
    console.log("Question info sent to Chat:", questionInfo);
  };

  const handleCloseModal = () => {
    setIsModalOpen(false);
  };

  return (
    <div className="main-container">
      <h2 className="advisor-heading">Advisor</h2>
      <UploadedDoc />
      <Chat onQuestionClick={handleQuestionClick} />
      <Insights selectedQuestion={selectedQuestion} onSendQuestionInfo={handleSendQuestionInfo} />
      
      <Modal isOpen={isModalOpen} onClose={handleCloseModal}>
        <h3>Welcome</h3>
        <p>Hello! This is your modal content.</p>
      </Modal>
    </div>
  );
}

export default MainContainer;



.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.5s ease-in-out;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
  animation: slideIn 0.5s ease-in-out;
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 10px;
  background: none;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes slideIn {
  from { transform: translateY(-50px); }
  to { transform: translateY(0); }
}





import React from "react";
import "./Modal.css";

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  return (
    <div className="modal-overlay">
      <div className="modal-content">
        <button className="modal-close" onClick={onClose}>
          &times;
        </button>
        {children}
      </div>
    </div>
  );
}

export default Modal;
