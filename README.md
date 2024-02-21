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
        background-color: #f0f8ff; /* 浅蓝色背景 */
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
    .comment-input {
        text-align: center;
        margin: 20px auto;
        width: 100%; /* 最大化输入框长度 */
    }
    input[type="text"] {
        padding: 10px;
        width: 100%; /* 最大化输入框长度 */
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
    .comments {
        margin: 20px auto;
        width: 100%; /* 最大化评论展示区域宽度 */
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
        background-color: #f9f9f9;
        border-radius: 5px;
    }
    .comment-item small {
        font-size: 14px;
        color: #888;
    }
    .comment-nickname {
        font-weight: bold;
        margin-right: 5px;
    }
    .delete-button {
        position: absolute;
        top: 5px;
        right: 5px;
        cursor: pointer;
        width: 15px;
        height: 15px;
    }
    .clear-comments {
        text-align: center;
        margin-top: 20px;
    }
</style>
</head>
<body>
<h1>郭的私密聊天室</h1>
<div class="comment-input">
    <input type="text" id="commentInput" placeholder="发表评论">
    <button onclick="addComment()">发表</button>
</div>
<div class="comments" id="commentsList"></div>
<div class="clear-comments">
    <button onclick="clearAllComments()" style="background-color: #ff0000;">
        一键删除
    </button>
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
        newComment.appendChild(commentContent);
        
        var deleteButton = document.createElement('img');
        deleteButton.classList.add('delete-button');
        deleteButton.src = 'https://img.icons8.com/ios-glyphs/15/008000/trash--v1.png';
        deleteButton.onclick = function() {
            commentsList.removeChild(newComment);
        };
        newComment.appendChild(deleteButton);

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

    function clearAllComments() {
        var commentsList = document.getElementById('commentsList');
        commentsList.innerHTML = '';
    }
</script>
</body>
</html>


温馨提示：
此空间不保留任何信息，关闭即删。
讲乜都无人可以追查，请放心鸠up！
