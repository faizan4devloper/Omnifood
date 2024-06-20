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
        <div>
          <label>Username:</label>
          <input 
            type="text" 
            value={username} 
            onChange={(e) => setUsername(e.target.value)} 
          />
        </div>
        <div>
          <label>Password:</label>
          <input 
            type="password" 
            value={password} 
            onChange={(e) => setPassword(e.target.value)} 
          />
        </div>
        <button type="submit">Login</button>
      </form>
    </div>
        </div>
  );
}





.login-container{
      background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
      height: 100vh;

}
.login-content {
  width: 300px;
  height: 300px;
  margin: 100px auto;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background:rgba(0, 0, 0, 0.5);
}

form {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
}

.login-content input {
  margin-bottom: 15px;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
