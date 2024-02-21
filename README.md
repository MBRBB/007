<html>
<head>
<style>
body {
  margin: 0;
  padding: 0;
}

#chatroom {
  text-align: center;
  font-weight: bold;
  background-color: #3498db; /* 蓝色背景 */
  color: white; /* 白色文字 */
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  padding: 10px 0;
  z-index: 1000; /* 保证主题区域位于最上层 */
}

#chat_messages {
  text-align: left;
  margin: 100px auto 0 auto; /* 居中显示，顶部留出空间给主题 */
  max-width: 600px; /* 限制留言板宽度 */
  padding: 20px;
  overflow-y: auto; /* 垂直滚动条 */
  max-height: calc(100vh - 200px); /* 最大高度，减去主题的高度 */
  z-index: 999; /* 保证留言展示区域位于主题下方 */
}

.message {
  background-color: #ffffcc; /* 浅黄色背景 */
  padding: 5px; /* 缩短留言框的高度 */
  margin-bottom: 5px; /* 减小留言之间的间隔 */
  position: relative; /* 相对定位 */
}

.deleteButton {
  position: absolute;
  top: 50%;
  right: 5px;
  transform: translateY(-50%); /* 垂直居中 */
  color: white; /* 白色文字 */
  border: none;
  padding: 5px;
  cursor: pointer;
  background-color: #7fff00; /* 浅绿色背景 */
}

.deleteButton img {
  width: 12.5px; /* 缩小垃圾桶图标大小一半 */
  background-color: transparent; /* 设置背景颜色为透明 */
}

#chat_input {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #f2f2f2;
  padding: 10px;
  box-sizing: border-box; /* 让内边距和边框计入总宽度 */
}

#messageInput {
  width: 80%; /* 文字输入框宽度 */
  padding: 8px; /* 内边距 */
  box-sizing: border-box; /* 让内边距和边框计入总宽度 */
  border: 1px solid #ccc; /* 边框 */
  border-radius: 4px; /* 圆角 */
}

#sendButton {
  width: 18%; /* 发送按钮宽度 */
  padding: 8px; /* 内边距 */
  box-sizing: border-box; /* 让内边距和边框计入总宽度 */
  border: none; /* 去掉边框 */
  background-color: #3498db; /* 蓝色背景 */
  color: white; /* 白色文字 */
  border-radius: 4px; /* 圆角 */
  cursor: pointer; /* 光标样式 */
}

</style>
</head>
<body>

<div id="chatroom">
  <h1>郭的私密聊天室</h1>
</div>

<div id="chat_messages">
  <!-- 留言信息显示区域 -->
</div>

<div id="chat_input">
  <input type="text" id="messageInput" placeholder="输入留言...">
  <button id="sendButton" onclick="sendMessage()">发送留言</button>
</div>

<script>
// 获取本地存储中的留言数据
let messages = JSON.parse(localStorage.getItem("messages")) || [];

// 显示留言信息
const chatMessages = document.getElementById("chat_messages");
messages.forEach((message, index) => {
  const messageDiv = document.createElement("div");
  messageDiv.classList.add("message");
  messageDiv.innerHTML = `<p>${message.content}</p><span>${message.time}</span><button class="deleteButton" onclick="deleteMessage(${index})"><img src="https://img.icons8.com/ios/50/000000/trash.png"/></button>`;
  chatMessages.appendChild(messageDiv);
});

// 发送留言
function sendMessage() {
  const messageInput = document.getElementById("messageInput");
  const newMessage = { content: messageInput.value, time: new Date().toLocaleTimeString() };
  messages.push(newMessage);
  localStorage.setItem("messages", JSON.stringify(messages)); // 将留言数据保存到本地存储

  const newMessageDiv = document.createElement("div");
  newMessageDiv.classList.add("message");
  newMessageDiv.innerHTML = `<p>${newMessage.content}</p><span>${newMessage.time}</span><button class="deleteButton" onclick="deleteMessage(${messages.length - 1})"><img src="https://img.icons8.com/ios/50/000000/trash.png"/></button>`;
  chatMessages.appendChild(newMessageDiv);
  messageInput.value = ""; // 清空输入框
  scrollToBottom();
}

// 删除留言
function deleteMessage(index) {
  messages.splice(index, 1);
  localStorage.setItem("messages", JSON.stringify(messages)); // 更新本地存储
  renderMessages();
}

// 渲染留言
function renderMessages() {
  chatMessages.innerHTML = "";
  messages.forEach((message, index) => {
    const messageDiv = document.createElement("div");
    messageDiv.classList.add("message");
    messageDiv.innerHTML = `<p>${message.content}</p><span>${message.time}</span><button class="deleteButton" onclick="deleteMessage(${index})"><img src="https://img.icons8.com/ios/50/000000/trash.png"/></button>`;
    chatMessages.appendChild(messageDiv);
  });
  scrollToBottom();
}

// 滚动到底部
function scrollToBottom() {
  chatMessages.scrollTop = chatMessages.scrollHeight;
}

// 在页面加载完成后，自动滚动到底部
window.onload = scrollToBottom;

</script>

</body>
</html>
