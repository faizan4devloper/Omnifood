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


const [selectedQuestion, setSelectedQuestion] = useState(null);

  return (
    <div className="app">
      <nav className="breadcrumbs">
        <ul>
          <li>
            <a href="#" onClick={handleGoBack} >
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
          <Chat onQuestionClick={setSelectedQuestion}/>
          <Insights setSelectedQuestion={setSelectedQuestion}/>
        </div>
      )}
    </div>
  );
}

export default App;
