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
