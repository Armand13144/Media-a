<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Zizz - Social App</title>
    <link rel="stylesheet" href="./style.css">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <header>
            <h1>Zizz</h1>
            <button id="logout-btn"><i class="fas fa-sign-out-alt"></i></button>
        </header>

        <!-- Post Form -->
        <div class="post-form">
            <textarea id="post-content" placeholder="What's buzzing?"></textarea>
            <button id="post-btn"><i class="fas fa-paper-plane"></i> Post</button>
        </div>

        <!-- Feed -->
        <div class="feed" id="feed">
            <!-- Posts will appear here -->
        </div>
    </div>

    <script src="./app.js"></script>
</body>
</html>
