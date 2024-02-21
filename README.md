<html>
<head>
<style>
#chatroom {
  text-align: center;
  font-weight: bold;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #f2f2f2;
  padding: 10px 0;
}

#chat_messages {
  text-align: left;
  margin: 50px 20px 20px 20px; /* 留出顶部空间给 chatroom */
}

#chat_input {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #f2f2f2;
  padding: 10px;
}
</style>
</head>
<body>

<div id="chatroom">
  <h1>郭的留言板</h1>
</div>

<div id="chat_messages">
  <!-- 留言信息显示区域 -->
</div>

<div id="chat_input">
  <input type="text" id="messageInput" placeholder="输入留言...">
  <button onclick="sendMessage()">发送留言</button>
</div>

<script>
// 留言相关的 JavaScript 代码
</script>

</body>
</html>
