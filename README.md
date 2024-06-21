import React, { useState } from "react";
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";

import { faUser, faLock } from "@fortawesome/free-solid-svg-icons";

import "./Login.css";

export function Login({ onLogin }) {
  const [username, setUsername] = useState("");
  const [password, setPassword] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    // Simple authentication check
    if (username === "test" && password === "1212") {
      onLogin();
    } else {
      alert("Invalid username or password");
    }
  };

  return (
    <div className="login-container">
      <div className="login-h">
       <h2>UK <br/> Citizen Advisor</h2>
      </div>
      <div className="login-content">
        <form onSubmit={handleSubmit}>
          <h2>Login</h2>
          <div className="input-group">
            <label>
              <FontAwesomeIcon className="icon" icon={faUser} /> Username
            </label>
            <input
              type="text"
              value={username}
              onChange={(e) => setUsername(e.target.value)}
              placeholder="Enter your username"
            />
          </div>
          <div className="input-group">
            <label>
              <FontAwesomeIcon className="icon" icon={faLock} /> Password
            </label>
            <input
              type="password"
              value={password}
              onChange={(e) => setPassword(e.target.value)}
              placeholder="Enter your password"
            />
          </div>
          <button type="submit">
            <i className="fas fa-sign-in-alt"></i> Login
          </button>
        </form>
      </div>
    </div>
  );
}










/* Login.css */

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
}

.login-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  max-width: 1200px;
  background: rgba(255, 255, 255, 0.1);
  backdrop-filter: blur(10px);
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

.login-container:hover {
  transform: scale(1.02);
  box-shadow: 0 15px 40px rgba(0, 0, 0, 0.3);
}

.login-h {
  flex: 1;
  text-align: center;
  color: #fff;
  animation: slideIn 1s ease-in-out;
}

.login-h h2 {
  font-size: 3rem;
  line-height: 1.2;
  margin: 0;
}

.login-content {
  flex: 1;
  max-width: 400px;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2), 0 6px 6px rgba(0, 0, 0, 0.23);
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
}

@keyframes slideIn {
  from {
    transform: translateX(-100%);
    opacity: 0;
  }
  to {
    transform: translateX(0);
    opacity: 1;
  }
}

form {
  display: flex;
  flex-direction: column;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.input-group {
  margin-bottom: 20px;
}

label {
  margin-bottom: 8px;
  font-size: 15px;
  color: #555;
  display: flex;
  align-items: center;
}

label .icon {
  margin-right: 8px;
}

.login-content input {
  width: 95%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
  transition: all 0.3s ease-in-out;
}

.login-content input:focus {
  border-color: #1f77f6;
  outline: none;
  box-shadow: 0 0 8px rgba(31, 119, 246, 0.6);
}

button {
  padding: 12px;
  border: none;
  border-radius: 4px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s ease-in-out, transform 0.3s ease-in-out;
}

button i {
  margin-right: 8px;
}

button:hover {
  background: linear-gradient(90deg, #5a2ba6 0%, #1559b3 100%);
  transform: scale(1.05);
}





/* Login.css */

.login-container {
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  height: 100vh;
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.login-content {
  width: 320px; /* Slightly increased width for a more spacious form */
  padding: 30px;
  border-radius: 12px;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2), 0 6px 6px rgba(0, 0, 0, 0.23); /* Updated box shadow */
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
}


form {
  display: flex;
  flex-direction: column;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: #333;
}

.input-group {
  margin-bottom: 20px;
}

label {
  margin-bottom: 8px;
  font-size: 15px;
  color: #555;
  display: flex;
  align-items: center;
}

label .icon {
  margin-right: 8px;
}

.login-content input {
  width: 95%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
  transition: all 0.3s ease-in-out; /* Smooth transition */
}

.login-content input:focus {
  border-color: #1f77f6;
  outline: none;
  box-shadow: 0 0 8px rgba(31, 119, 246, 0.6);
}

button {
  padding: 12px;
  border: none;
  border-radius: 4px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background 0.3s ease-in-out, transform 0.3s ease-in-out; /* Smooth transition */
}

button i {
  margin-right: 8px;
}

button:hover {
  background: linear-gradient(90deg, #5a2ba6 0%, #1559b3 100%);
  transform: scale(1.05); /* Slightly enlarge button on hover */
}
