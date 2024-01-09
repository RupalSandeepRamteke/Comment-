
* {

margin: 0;

padding: 0;

text-decoration: none;

}

a {

color: rgb(51, 204, 51);

}

#header {

background: black;

}

#footer {

background: yellow;

}




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






import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';

const Login: React.FC = () => {
  const [userId, setUserId] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState<string>('');
  const navigate = useNavigate();

  const handleLogin = () => {
    // Basic validation
    if (userId.trim() === '' || password.trim() === '') {
      setError('Please enter both User ID and Password.');
      return;
    }

    // Simulated user authentication using local browser storage
    const storedUserId = localStorage.getItem('userId');
    const storedPassword = localStorage.getItem('password');

    if (userId === storedUserId && password === storedPassword) {
      navigate('/comments');
    } else {
      setError('Invalid credentials. Please try again.');
    }
  };

  return (
    <div>
      <h2>Login</h2>
      <input
        type="text"
        placeholder="User ID"
        value={userId}
        onChange={(e) => setUserId(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={handleLogin}>Login</button>
      {error && <p style={{ color: 'red' }}>{error}</p>}
    </div>
  );
};

export default Login;
..................................

import React, { useState } from 'react';
import { useNavigate } from 'react-router-dom';

// Array of user credentials
const userCredentials = [
  {
    userId: 'user1',
    password: 'password1'
  },
  {
    userId: 'user2',
    password: 'password2'
  },
  // Add more user objects as needed
];

const Login: React.FC = () => {
  const [userId, setUserId] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState<string>('');

  const navigate = useNavigate();

  const handleLogin = () => {
    // Basic validation
    if (userId.trim() === '' || password.trim() === '') {
      setError('Please enter both User ID and Password.');
      return;
    }

    // Check user credentials from the userCredentials array
    const user = userCredentials.find(user => user.userId === userId);

    if (user && user.password === password) {
      navigate('/comments');
    } else {
      setError('Invalid credentials. Please try again.');
    }
  };

  return (
    <div>
      <h2>Login</h2>
      <input
        type="text"
        placeholder="User ID"
        value={userId}
        onChange={(e) => setUserId(e.target.value)}
      />
      <input
        type="password"
        placeholder="Password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
      />
      <button onClick={handleLogin}>Login</button>
      {error && <p style={{ color: 'red' }}>{error}</p>}
    </div>
  );
};


export default Login;












