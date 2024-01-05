import React from 'react';
import './App.css';
import LoginPage from './components/LoginPage';

function App() {
  return (
    <div className="App">
      <LoginPage />
    </div>
  );
}

export default App;


...............................


import React, { useState } from 'react';

const LoginPage = () => {
  const [username, setUsername] = useState('');
  const [password, setPassword] = useState('');

  const handleLogin = () => {
    // Handle login logic here, you can authenticate the user with entered credentials
    console.log(`Username: ${username}, Password: ${password}`);
  };

  return (
    <div className="login-container">
      <div className="input-div">
        <label htmlFor="username">Username</label>
        <input
          type="text"
          id="username"
          value={username}
          onChange={(e) => setUsername(e.target.value)}
        />
      </div>
      <div className="input-div">
        <label htmlFor="password">Password</label>
        <input
          type="password"
          id="password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
        />
      </div>
      <div className="button-div">
        <button onClick={handleLogin}>Login</button>
      </div>
    </div>
  );
};

export default LoginPage;





/* styles.css */

body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  width: 400px;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h2 {
  margin-bottom: 20px;
}

form {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
}

input {
  padding: 8px;
  margin-bottom: 15px;
  border-radius: 3px;
  border: 1px solid #ccc;
  font-size: 14px;
}

button {
  padding: 10px 15px;
  border: none;
  border-radius: 3px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
  font-size: 14px;
}

button:hover {
  background-color: #0056b3;
}
