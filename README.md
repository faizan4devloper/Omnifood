import React, { useState } from "react";
import './App.css';
import { UploadedDoc } from "./components/UploadedDoc";
import { Chat } from "./components/Chat";
import { Insights } from "./components/Insights";
import { Login } from "./components/Login";
import { Landing } from "./components/Landing";

function App() {
  const [view, setView] = useState('login'); // 'login', 'landing', 'main'

  const handleLogin = () => {
    setView('landing');
  };

  const handleEnterMain = () => {
    setView('main');
  };

  return (
    <div className="app">
      {view === 'login' && <Login onLogin={handleLogin} />}
      {view === 'landing' && <Landing onEnterMain={handleEnterMain} />}
      {view === 'main' && (
        <div className="main-container">
          <UploadedDoc />
          <Chat />
          <Insights />
        </div>
      )}
    </div>
  );
}

export default App;
















@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap");

body,
html {
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  margin: 0;
  padding: 0;
  font-family: "Poppins", Arial, sans-serif;
  scroll-behavior: smooth;
  overflow: auto;
  overflow-x: hidden;
  -webkit-overflow-scrolling: touch;
}
body::-webkit-scrollbar {
  width: 0px; /* Remove the scrollbar width */
  background: transparent; /* Optional: Just to ensure transparency */
}
.main-container{
  display: flex;
  justify-content: space-between;
  /*height: 100vh;*/
  /*align-items: center;*/
}






import React from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faArrowRight } from "@fortawesome/free-solid-svg-icons";
import "./Landing.css";

export function Landing({ onEnterMain }) {
  return (
    <div className="landing">
      <h2 onClick={onEnterMain}>UK Citizen Advisor</h2>
      <div className="cards-container">
        <div className="card">
          <h4>Education Advisor</h4>
          <p>Description about Education Advisor.</p>
          <button onClick={onEnterMain}>
<FontAwesomeIcon icon={faArrowRight} />
</button>
        </div>
        <div className="card">
          <h4>Job Advisor</h4>
          <p>Description about Job Advisor.</p>
          <button onClick={onEnterMain}>
<FontAwesomeIcon icon={faArrowRight} />
</button>
        </div>
        <div className="card">
          <h4>Health Advisor</h4>
          <p>Description about Health Advisor.</p>
          <button onClick={onEnterMain}>
<FontAwesomeIcon icon={faArrowRight} />
</button>
        </div>
      </div>
    </div>
  );
}
