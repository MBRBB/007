<html>
<head>
<style>
#chatroom {
  text-align: center;
  font-weight: bold;
}
#chat_messages {
  text-align: left;
  margin: 20px;
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
// 获取本地存储中的留言数据
let messages = JSON.parse(localStorage.getItem("messages")) || [];

// 显示留言信息
const chatMessages = document.getElementById("chat_messages");
messages.forEach(message => {
  const messageDiv = document.createElement("div");
  messageDiv.innerHTML = `<p>${message.content}</p><span>${message.time}</span>`;
  chatMessages.appendChild(messageDiv);
});

// 发送留言
function sendMessage() {
  const messageInput = document.getElementById("messageInput");
  const newMessage = { content: messageInput.value, time: new Date().toLocaleTimeString() };
  messages.push(newMessage);
  localStorage.setItem("messages", JSON.stringify(messages)); // 将留言数据保存到本地存储

  const newMessageDiv = document.createElement("div");
  newMessageDiv.innerHTML = `<p>${newMessage.content}</p><span>${newMessage.time}</span>`;
  chatMessages.appendChild(newMessageDiv);
  messageInput.value = ""; // 清空输入框
}
</script>

</body>
</html>
