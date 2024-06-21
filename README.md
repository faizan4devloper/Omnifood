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
  padding: 5px;
}

.breadcrumbs ul li a:hover {
  color: #1f77f6; /* Change color on hover */
}

.breadcrumbs ul li span {
  color: #777;
  padding: 5px;
}

.breadcrumbs ul li.active a {
  color: #1f77f6; /* Change color for active breadcrumb */
}

.breadcrumbs ul li.active a:hover {
  color: #1559b3; /* Change color for active breadcrumb on hover */
}




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
          {view === 'landing' && <li><span> / Landing</span></li>}
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
          <li>
            <a href="#" onClick={handleGoBack}>
              <i className="fas fa-home"></i> Home
            </a>
          </li>
          {view === 'main' && (
            <>
              <li>
                <span> / </span>
              </li>
              <li>
                <a href="#">
                  {advisorType} Advisor
                </a>
              </li>
            </>
          )}
          {view === 'landing' && (
            <li>
              <span> / </span>
              <span>Landing</span>
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
          <Chat />
          <Insights />
        </div>
      )}
    </div>
  );
}

export default App;
