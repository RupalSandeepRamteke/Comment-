import React, { useState } from 'react';

interface Comment {
  id: number;
  text: string;
  replies: Comment[];
}

const CommentSection: React.FC = () => {
  const [comments, setComments] = useState<Comment[]>([]);
  const [newComment, setNewComment] = useState<string>('');

  const handleAddComment = () => {
    // Logic to add a top-level comment
    const comment: Comment = {
      id: comments.length + 1,
      text: newComment,
      replies: [],
    };
    setComments([...comments, comment]);
    setNewComment('');
  };

  const handleAddReply = (parentId: number) => (replyText: string) => {
    // Logic to add a reply to a specific comment
    const updatedComments = comments.map(comment => {
      if (comment.id === parentId) {
        return {
          ...comment,
          replies: [
            ...comment.replies,
            {
              id: comment.replies.length + 1,
              text: replyText,
              replies: [],
            },
          ],
        };
      }
      return comment;
    });

    setComments(updatedComments);
  };

  const renderComments = (commentList: Comment[]) => {
    return commentList.map(comment => (
      <div key={comment.id}>
        <p>{comment.text}</p>
        <input
          type="text"
          placeholder="Reply..."
          value={newComment}
          onChange={(e) => setNewComment(e.target.value)}
        />
        <button onClick={() => handleAddReply(comment.id)(newComment)}>
          Add Reply
        </button>
        {comment.replies.length > 0 && renderComments(comment.replies)}
      </div>
    ));
  };

  return (
    <div>
      <h2>Comments</h2>
      <input
        type="text"
        placeholder="Add a comment..."
        value={newComment}
        onChange={(e) => setNewComment(e.target.value)}
      />
      <button onClick={handleAddComment}>Add Comment</button>
      {comments.length > 0 && renderComments(comments)}
    </div>
  );
};

export default CommentSection;













import React, { useState } from 'react';

interface LoginProps {
  setLoggedIn: React.Dispatch<React.SetStateAction<boolean>>;
}

const Login: React.FC<LoginProps> = ({ setLoggedIn }) => {
  const [userId, setUserId] = useState('');
  const [password, setPassword] = useState('');
  const [error, setError] = useState<string>('');

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
      setLoggedIn(true);
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

















import React, { useState } from 'react';
import './App.css';
import Login from './components/Login';
import CommentSection from './components/CommentSection';

const App: React.FC = () => {
  const [loggedIn, setLoggedIn] = useState<boolean>(false);

  return (
    <div className="App">
      {!loggedIn ? (
        <Login setLoggedIn={setLoggedIn} />
      ) : (
        <CommentSection />
      )}
    </div>
  );
};

export default App;
