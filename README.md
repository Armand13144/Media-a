<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zizz Social App</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', sans-serif;
        }
        body {
            background-color: #f5f5f5;
            color: #333;
        }
        .app-container {
            max-width: 600px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            padding-bottom: 10px;
            border-bottom: 1px solid #ddd;
        }
        header h1 {
            color: #ff6b6b;
            font-size: 28px;
        }
        #logout-btn {
            background: none;
            border: none;
            color: #ff6b6b;
            font-size: 20px;
            cursor: pointer;
        }
        .post-form {
            background: white;
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        .post-form textarea {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            resize: none;
            margin-bottom: 10px;
            min-height: 100px;
            font-size: 16px;
        }
        #post-btn {
            background-color: #ff6b6b;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
        }
        .post {
            background: white;
            margin-bottom: 20px;
            border-radius: 10px;
            padding: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .post-header {
            display: flex;
            align-items: center;
            margin-bottom: 10px;
        }
        .post-user {
            font-weight: bold;
            margin-left: 10px;
        }
        .post-time {
            color: #999;
            font-size: 12px;
            margin-left: auto;
        }
        .post-content {
            margin-bottom: 15px;
            line-height: 1.5;
        }
        .post-actions {
            display: flex;
            border-top: 1px solid #eee;
            padding-top: 10px;
        }
        .post-action {
            margin-right: 15px;
            color: #555;
            cursor: pointer;
        }
        .post-action i {
            margin-right: 5px;
        }
    </style>
</head>
<body>
    <div class="app-container">
        <header>
            <h1>Zizz</h1>
            <button id="logout-btn"><i class="fas fa-sign-out-alt"></i></button>
        </header>

        <div class="post-form">
            <textarea id="post-content" placeholder="What's buzzing?"></textarea>
            <button id="post-btn"><i class="fas fa-paper-plane"></i> Post</button>
        </div>

        <div class="feed" id="feed">
            <!-- Posts will appear here -->
        </div>
    </div>

    <!-- Font Awesome for icons -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/js/all.min.js"></script>
    
    <script>
        // Mock user data
        let currentUser = "Guest";
        let posts = [
            { 
                id: 1, 
                user: "ZizzTeam", 
                content: "Welcome to Zizz! Post something awesome!", 
                likes: 10, 
                time: "Just now" 
            }
        ];

        // DOM Elements
        const postContent = document.getElementById('post-content');
        const postBtn = document.getElementById('post-btn');
        const feed = document.getElementById('feed');
        const logoutBtn = document.getElementById('logout-btn');

        // Render all posts
        function renderPosts() {
            feed.innerHTML = posts.map(post => `
                <div class="post" data-id="${post.id}">
                    <div class="post-header">
                        <i class="fas fa-user-circle"></i>
                        <span class="post-user">${post.user}</span>
                        <span class="post-time">${post.time}</span>
                    </div>
                    <div class="post-content">
                        ${post.content}
                    </div>
                    <div class="post-actions">
                        <div class="post-action" onclick="likePost(${post.id})">
                            <i class="far fa-heart"></i>
                            <span>${post.likes}</span>
                        </div>
                        <div class="post-action">
                            <i class="far fa-comment"></i>
                            <span>0</span>
                        </div>
                    </div>
                </div>
            `).join('');
        }

        // Add a new post
        function addPost() {
            const content = postContent.value.trim();
            if (content) {
                const newPost = {
                    id: Date.now(),
                    user: currentUser,
                    content: content,
                    likes: 0,
                    time: "Just now"
                };
                posts.unshift(newPost);
                postContent.value = '';
                renderPosts();
            }
        }

        // Like a post
        function likePost(postId) {
            const post = posts.find(p => p.id === postId);
            if (post) {
                post.likes++;
                renderPosts();
            }
        }

        // Event Listeners
        postBtn.addEventListener('click', addPost);
        postContent.addEventListener('keypress', (e) => {
            if (e.key === 'Enter' && !e.shiftKey) {
                e.preventDefault();
                addPost();
            }
        });

        logoutBtn.addEventListener('click', () => {
            alert("Logout functionality would go here!");
        });

        // Initialize
        renderPosts();
    </script>
</body>
</html>
