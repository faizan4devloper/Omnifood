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

  const handleGoBack = () => {
    if (view === 'landing') {
      setView('login');
    } else if (view === 'main') {
      setView('landing');
    }
  };

  return (
    <div className="app">
      <nav className="breadcrumbs">
        <ul>
          <li><a href="#" onClick={handleGoBack}>Home</a></li>
          {view === 'main' && <li><span> / {advisorType} Advisor</span></li>}
        </ul>
      </nav>
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










/* App.css */

.breadcrumbs {
  background-color: #f2f2f2;
  padding: 10px;
}

.breadcrumbs ul {
  list-style-type: none;
  margin: 0;
  padding: 0;
}

.breadcrumbs ul li {
  display: inline;
}

.breadcrumbs ul li:not(:first-child)::before {
  content: ">";
  margin: 0 5px;
}

.breadcrumbs ul li a {
  text-decoration: none;
  color: #333;
}

.breadcrumbs ul li span {
  color: #777;
}
