# Media-a
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>SocialApp</title>
    <link rel="stylesheet" href="style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Firebase SDK -->
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-app.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-auth.js"></script>
    <script src="https://www.gstatic.com/firebasejs/8.10.0/firebase-firestore.js"></script>
</head>
<body>
    <div class="auth-container" id="auth-container">
        <div class="auth-box">
            <h1>SocialApp</h1>
            <input type="email" id="email" placeholder="Email">
            <input type="password" id="password" placeholder="Password">
            <button id="login-btn">Login</button>
            <button id="signup-btn">Sign Up</button>
            <p id="auth-message"></p>
        </div>
    </div>

    <div class="app-container" id="app-container" style="display: none;">
        <header>
            <h1>SocialApp</h1>
            <button id="logout-btn">Logout</button>
        </header>

        <div class="post-form">
            <textarea id="post-content" placeholder="What's on your mind?"></textarea>
            <button id="post-btn">Post</button>
        </div>

        <div class="feed" id="feed">
            <!-- Posts will appear here -->
        </div>
    </div>

    <script src="app.js"></script>
</body>
</html> 
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

body {
    background-color: #f5f5f5;
    color: #333;
}

.auth-container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    background-color: #0095f6;
}

.auth-box {
    background: white;
    padding: 2rem;
    border-radius: 8px;
    width: 350px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    text-align: center;
}

.auth-box h1 {
    margin-bottom: 1.5rem;
    color: #0095f6;
}

.auth-box input {
    width: 100%;
    padding: 12px;
    margin-bottom: 1rem;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
}

.auth-box button {
    width: 100%;
    padding: 12px;
    margin-bottom: 0.5rem;
    border: none;
    border-radius: 4px;
    font-size: 1rem;
    cursor: pointer;
}

#login-btn {
    background-color: #0095f6;
    color: white;
}

#signup-btn {
    background-color: transparent;
    color: #0095f6;
    border: 1px solid #0095f6;
}

#auth-message {
    color: red;
    margin-top: 1rem;
    min-height: 20px;
}

.app-container {
    max-width: 600px;
    margin: 0 auto;
    padding: 1rem;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 1.5rem;
}

#logout-btn {
    background: none;
    border: none;
    color: #0095f6;
    cursor: pointer;
    font-size: 1rem;
}

.post-form {
    margin-bottom: 2rem;
    background: white;
    padding: 1rem;
    border-radius: 8px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.post-form textarea {
    width: 100%;
    padding: 12px;
    border: 1px solid #ddd;
    border-radius: 4px;
    resize: none;
    margin-bottom: 1rem;
    min-height: 100px;
    font-size: 1rem;
}

#post-btn {
    background-color: #0095f6;
    color: white;
    border: none;
    padding: 10px 20px;
    border-radius: 4px;
    cursor: pointer;
    font-size: 1rem;
}

.post {
    background: white;
    margin-bottom: 1.5rem;
    border-radius: 8px;
    padding: 1rem;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.post-header {
    display: flex;
    align-items: center;
    margin-bottom: 1rem;
}

.post-user {
    font-weight: bold;
    margin-left: 10px;
}

.post-time {
    color: #999;
    font-size: 0.8rem;
    margin-left: auto;
}

.post-content {
    margin-bottom: 1rem;
    line-height: 1.5;
}

.post-actions {
    display: flex;
    border-top: 1px solid #eee;
    padding-top: 0.5rem;
}

.post-action {
    display: flex;
    align-items: center;
    margin-right: 1rem;
    color: #555;
    cursor: pointer;
}

.post-action i {
    margin-right: 5px;
}

.comments {
    margin-top: 1rem;
    border-top: 1px solid #eee;
    padding-top: 1rem;
}

.comment {
    margin-bottom: 0.5rem;
    display: flex;
}

.comment-user {
    font-weight: bold;
    margin-right: 5px;
}

.comment-form {
    display: flex;
    margin-top: 1rem;
}

.comment-input {
    flex: 1;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
}

.comment-btn {
    background-color: #0095f6;
    color: white;
    border: none;
    padding: 8px 12px;
    border-radius: 4px;
    margin-left: 8px;
    cursor: pointer;
}
// Firebase configuration (replace with your own)
const firebaseConfig = {
    apiKey: "AIzaSyDEXAMPLEEXAMPLEEXAMPLE",
    authDomain: "yourapp.firebaseapp.com",
    projectId: "yourapp",
    storageBucket: "yourapp.appspot.com",
    messagingSenderId: "1234567890",
    appId: "1:1234567890:web:abc123def456"
};

// Initialize Firebase
firebase.initializeApp(firebaseConfig);
const auth = firebase.auth();
const db = firebase.firestore();

// DOM elements
const authContainer = document.getElementById('auth-container');
const appContainer = document.getElementById('app-container');
const emailInput = document.getElementById('email');
const passwordInput = document.getElementById('password');
const loginBtn = document.getElementById('login-btn');
const signupBtn = document.getElementById('signup-btn');
const authMessage = document.getElementById('auth-message');
const logoutBtn = document.getElementById('logout-btn');
const postContent = document.getElementById('post-content');
const postBtn = document.getElementById('post-btn');
const feed = document.getElementById('feed');

let currentUser = null;

// Auth state listener
auth.onAuthStateChanged(user => {
    if (user) {
        // User is signed in
        currentUser = user;
        authContainer.style.display = 'none';
        appContainer.style.display = 'block';
        loadPosts();
    } else {
        // No user is signed in
        currentUser = null;
        authContainer.style.display = 'flex';
        appContainer.style.display = 'none';
    }
});

// Login function
loginBtn.addEventListener('click', () => {
    const email = emailInput.value;
    const password = passwordInput.value;
    
    auth.signInWithEmailAndPassword(email, password)
        .catch(error => {
            authMessage.textContent = error.message;
        });
});

// Signup function
signupBtn.addEventListener('click', () => {
    const email = emailInput.value;
    const password = passwordInput.value;
    
    auth.createUserWithEmailAndPassword(email, password)
        .catch(error => {
            authMessage.textContent = error.message;
        });
});

// Logout function
logoutBtn.addEventListener('click', () => {
    auth.signOut();
});

// Create post function
postBtn.addEventListener('click', () => {
    const content = postContent.value.trim();
    
    if (content) {
        db.collection('posts').add({
            userId: currentUser.uid,
            userEmail: currentUser.email,
            content: content,
            likes: [],
            comments: [],
            createdAt: firebase.firestore.FieldValue.serverTimestamp()
        }).then(() => {
            postContent.value = '';
        }).catch(error => {
            console.error("Error adding post: ", error);
        });
    }
});

// Load posts in real-time
function loadPosts() {
    db.collection('posts')
        .orderBy('createdAt', 'desc')
        .onSnapshot(snapshot => {
            feed.innerHTML = '';
            
            snapshot.forEach(doc => {
                const post = doc.data();
                const postId = doc.id;
                
                const postElement = document.createElement('div');
                postElement.className = 'post';
                postElement.dataset.id = postId;
                
                // Format timestamp
                const time = post.createdAt ? 
                    new Date(post.createdAt.seconds * 1000).toLocaleString() : 
                    'Just now';
                
                postElement.innerHTML = `
                    <div class="post-header">
                        <i class="fas fa-user-circle"></i>
                        <span class="post-user">${post.userEmail}</span>
                        <span class="post-time">${time}</span>
                    </div>
                    <div class="post-content">
                        ${post.content}
                    </div>
                    <div class="post-actions">
                        <div class="post-action like-btn">
                            <i class="far fa-heart"></i>
                            <span>${post.likes ? post.likes.length : 0}</span>
                        </div>
                        <div class="post-action comment-btn">
                            <i class="far fa-comment"></i>
                            <span>${post.comments ? post.comments.length : 0}</span>
                        </div>
                    </div>
                    <div class="comments" id="comments-${postId}">
                        ${renderComments(post.comments)}
                    </div>
                    <div class="comment-form">
                        <input type="text" class="comment-input" placeholder="Write a comment...">
                        <button class="comment-submit">Post</button>
                    </div>
                `;
                
                feed.appendChild(postElement);
                
                // Add like functionality
                const likeBtn = postElement.querySelector('.like-btn');
                likeBtn.addEventListener('click', () => {
                    toggleLike(postId, currentUser.uid);
                });
                
                // Add comment functionality
                const commentForm = postElement.querySelector('.comment-form');
                commentForm.addEventListener('submit', (e) => {
                    e.preventDefault();
                    const commentInput = commentForm.querySelector('.comment-input');
                    const comment = commentInput.value.trim();
                    
                    if (comment) {
                        addComment(postId, currentUser.uid, currentUser.email, comment);
                        commentInput.value = '';
                    }
                });
            });
        });
}

// Render comments
function renderComments(comments) {
    if (!comments || comments.length === 0) return '';
    
    return comments.map(comment => `
        <div class="comment">
            <span class="comment-user">${comment.userEmail}:</span>
            <span class="comment-text">${comment.text}</span>
        </div>
    `).join('');
}

// Toggle like function
function toggleLike(postId, userId) {
    const postRef = db.collection('posts').doc(postId);
    
    db.runTransaction(transaction => {
        return transaction.get(postRef).then(postDoc => {
            if (!postDoc.exists) {
                throw "Document does not exist!";
            }
            
            const post = postDoc.data();
            const likes = post.likes || [];
            const likeIndex = likes.indexOf(userId);
            
            if (likeIndex === -1) {
                likes.push(userId);
            } else {
                likes.splice(likeIndex, 1);
            }
            
            transaction.update(postRef, { likes: likes });
        });
    }).catch(error => {
        console.error("Transaction failed: ", error);
    });
}

// Add comment function
function addComment(postId, userId, userEmail, text) {
    const postRef = db.collection('posts').doc(postId);
    const comment = {
        userId: userId,
        userEmail: userEmail,
        text: text,
        createdAt: firebase.firestore.FieldValue.serverTimestamp()
    };
    
    postRef.update({
        comments: firebase.firestore.FieldValue.arrayUnion(comment)
    }).catch(error => {
        console.error("Error adding comment: ", error);
    });
}
