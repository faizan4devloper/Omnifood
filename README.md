import React, { useState } from "react";
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
      <div className="login-content">
        <form onSubmit={handleSubmit}>
          <h2>Login</h2>
          <div className="input-group">
            <label>
              <i className="fas fa-user"></i> Username
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
              <i className="fas fa-lock"></i> Password
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

.login-container {
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.login-content {
  width: 300px;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background: rgba(255, 255, 255, 0.9);
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
  margin-bottom: 15px;
}

label {
  margin-bottom: 5px;
  font-size: 14px;
  color: #666;
  display: flex;
  align-items: center;
}

label i {
  margin-right: 8px;
}

.login-content input {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  font-size: 14px;
  color: #333;
}

.login-content input:focus {
  border-color: #1f77f6;
  outline: none;
}

button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
}

button i {
  margin-right: 8px;
}

button:hover {
  background: linear-gradient(90deg, #5a2ba6 0%, #1559b3 100%);
}
