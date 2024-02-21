<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>郭的私密聊天室</title>
<style>
    body {
        margin: 0;
        padding: 0;
        font-family: 'Arial', sans-serif;
        background-color: #f2f2f2; /* 更柔和的灰色背景 */
        color: #333;
    }
    h1 {
        font-size: 2em;
        font-weight: bold;
        color: #0077cc;
        text-align: center;
        padding: 20px 0;
        margin: 0;
        background-color: #fff;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
    }
    .comments {
        margin: 20px auto;
        width: 80%; /* 设置评论展示区域宽度 */
        padding: 20px;
        background-color: #fff;
        border-radius: 10px;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        overflow: auto;
        max-height: 400px;
    }
    .comment-item {
        position: relative;
        padding: 10px;
        margin: 10px 0;
        background-color: #fff8dc; /* 浅黄色背景 */
        border-radius: 5px;
        box-shadow: 0 1px 2px rgba(0, 0, 0, 0.1); /* 添加细微阴影效果 */
        display: flex;
        justify-content: space-between;
        align-items: center;
    }
    .comment-item small {
        font-size: 12px; /* 缩小发表时间字体大小 */
        color: #777; /* 更浅的灰色 */
    }
    .delete-btn {
        background-color: transparent; /* 去掉背景色 */
        color: #ffd700; /* 黄色 */
        border: none;
        border-radius: 50%;
        padding: 5px;
        cursor: pointer;
    }
    .delete-btn:hover {
        color: #eec900; /* 深黄色 */
    }
    .comment-text {
        flex: 1;
    }
    .comment-input {
        text-align: center;
        margin: 20px auto; /* 设置输入框与评论展示区域之间的间距 */
        width: 80%; /* 设置输入框宽度 */
    }
    input[type="text"] {
        padding: 10px;
        width: 70%; /* 调整输入框宽度 */
        border: 1px solid #ccc;
        border-radius: 5px;
        font-size: 16px;
    }
    button {
        padding: 10px 20px;
        background-color: #0077cc;
        color: #fff;
        border: none;
        border-radius: 5px;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    button:hover {
        background-color: #0056b3;
    }
</style>
</head>
<body>
<h1>郭的私密聊天室</h1>
<div class="comments" id="commentsList"></div>
<div class="comment-input">
    <input type="text" id="commentInput" placeholder="发表评论">
    <button onclick="addComment()">发表</button>
</div>

<script>
    var commentId = 0;

    function addComment() {
        var commentInput = document.getElementById('commentInput');
        var commentText = commentInput.value;
        if (commentText.trim() === '') {
            alert('请输入评论');
            return;
        }

        commentText = parseEmojis(commentText);

        var commentsList = document.getElementById('commentsList');
        var newComment = document.createElement('div');
        newComment.classList.add('comment-item');
        
        var commentContent = document.createElement('span');
        var currentTime = new Date();
        var formattedTime = currentTime.toLocaleString(); // 获取格式化的时间字符串
        commentContent.innerHTML = 'A: ' + commentText + '<br>' + '<small>' + formattedTime + '</small>'; // 在评论后添加时间
        commentContent.classList.add('comment-text');
        newComment.appendChild(commentContent);

        var deleteBtn = document.createElement('button');
        deleteBtn.classList.add('delete-btn');
        deleteBtn.innerHTML = '&#128465;'; // 垃圾桶图标
        deleteBtn.onclick = function() {
            commentsList.removeChild(newComment);
        };
        newComment.appendChild(deleteBtn);

        commentsList.appendChild(newComment);

        commentInput.value = '';

        commentsList.scrollTop = commentsList.scrollHeight;

        commentId++;
    }

    function parseEmojis(text) {
        text = text.replace(':)', '😊');
        text = text.replace(':(', '😢');
        text = text.replace(':D', '😄');

        return text;
    }
</script>
</body>
</html>
