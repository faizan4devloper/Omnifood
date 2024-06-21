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

  const handleLogin = () => {
    setView('landing');
  };

  const handleEnterMain = (type) => {
    setAdvisorType(type);
    setView('main');
  };

  return (
    <div className="app">
      {view === 'login' && <Login onLogin={handleLogin} />}
      {view === 'landing' && <Landing onEnterMain={handleEnterMain} />}
      {view === 'main' && (
        <div className="main-container">
          <h2 className="advisor-heading">{advisorType} Advisor</h2>
          <UploadedDoc />
          <Chat />
          <Insights />
        </div>
      )}
    </div>
  );
}

export default App;












import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faArrowRight } from "@fortawesome/free-solid-svg-icons";
import "./Landing.css";

export function Landing({ onEnterMain }) {
  return (
    <div className="landing">
      <h2>UK Citizen Advisor</h2>
      <div className="cards-container">
        <div className="card">
          <h4>Education Advisor</h4>
          <p>Description about Education Advisor.</p>
          <button onClick={() => onEnterMain('Education')}>
            <FontAwesomeIcon icon={faArrowRight} />
          </button>
        </div>
        <div className="card">
          <h4>Job Advisor</h4>
          <p>Description about Job Advisor.</p>
          <button onClick={() => onEnterMain('Job')}>
            <FontAwesomeIcon icon={faArrowRight} />
          </button>
        </div>
        <div className="card">
          <h4>Health Advisor</h4>
          <p>Description about Health Advisor.</p>
          <button onClick={() => onEnterMain('Health')}>
            <FontAwesomeIcon icon={faArrowRight} />
          </button>
        </div>
      </div>
    </div>
  );
}










/* App.css */

.main-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  /* height: 100vh; */
  /* justify-content: space-between; */
}

.advisor-heading {
  font-size: 2rem;
  margin: 20px 0;
  color: #333; /* Color for the heading */
}
