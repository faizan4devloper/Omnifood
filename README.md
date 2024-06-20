/* Login.css */

.login-container {
  background: linear-gradient(90deg, #6f36cd 0%, #1f77f6 100%);
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.login-content {
  width: 350px; /* Slightly increased width for a more spacious form */
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
