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
        width: 20%; /* 缩短五分之一 */
    }
    input[type="text"] {
        padding: 10px;
        width: 100%; /* 自适应屏幕宽度 */
        border: 1px solid #ccc;
        border-radius: 5px;
        font-size: 16px;
    }
    button {
        padding: 5px 10px; /* 缩小一倍 */
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
        width: 20%; /* 缩短五分之一 */
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
        font-size: 14px; /* 缩小字体大小为14px */
        color: #888; /* 将时间颜色改为浅灰色 */
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
        width: 7.5px; /* 缩小一倍 */
        height: 7.5px; /* 缩小一倍 */
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

        // 将表情文本转换为对应的表情图标
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
        deleteButton.src = 'https://img.icons8.com/ios-glyphs/15/008000/trash--v1.png'; // 绿色垃圾桶图标
        deleteButton.onclick = function() {
            commentsList.removeChild(newComment);
        };
        newComment.appendChild(deleteButton);

        commentsList.appendChild(newComment);

        commentInput.value = '';

        // 滑动到最新评论处
        commentsList.scrollTop = commentsList.scrollHeight;

        commentId++;
    }

    // 函数用于将表情文本转换为对应的表情图标
    function parseEmojis(text) {
        // 在实际应用中，您可能需要使用专门的表情库或API进行转换
        // 这里简单地替换示例文本中的表情代码
        text = text.replace(':)', '😊');
        text = text.replace(':(', '😢');
        text = text.replace(':D', '😄');

        return text;
    }

    function clearAllComments() {
        var commentsList = document.getElementById('commentsList');
        commentsList.innerHTML = ''; // 清空评论
    }
</script>
</body>
</html>
