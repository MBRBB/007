<!DOCTYPE html>
<html lang="zh-CN">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>郭的私密聊天室</title>
<style>
  body {
    font-family: Arial, sans-serif;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
  }
  #chat-container {
    max-width: 600px;
    margin: 50px auto;
    background-color: #ffffff;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
    padding: 20px;
    position: relative;
  }
  #chat-title {
    text-align: center;
    color: #007bff;
    font-weight: bold;
    margin-bottom: 20px;
  }
  #messages {
    overflow-y: auto;
    max-height: 300px;
    margin-bottom: 20px;
    padding-right: 20px;
  }
  .message {
    margin-bottom: 10px;
    padding: 10px;
    border-radius: 5px;
    background-color: #f2f2f2;
    position: relative;
  }
  .message .time {
    font-size: 12px;
    color: #888888;
    position: absolute;
    top: 5px;
    right: 10px;
  }
  #input-message {
    width: calc(100% - 40px);
    padding: 10px;
    border: 1px solid #dddddd;
    border-radius: 5px;
    margin-right: 10px;
    margin-bottom: 10px;
  }
  #send-button {
    padding: 10px 20px;
    background-color: #007bff;
    color: #ffffff;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
</style>
</head>
<body>

<div id="chat-container">
  <div id="chat-title">郭的私密聊天室</div>
  <div id="messages"></div>
  <input type="text" id="input-message" placeholder="输入你的消息...">
  <button id="send-button">发送</button>
</div>

<script>
  const messagesContainer = document.getElementById('messages');
  const inputMessage = document.getElementById('input-message');
  const sendButton = document.getElementById('send-button');

  // Function to add a message to the chat
  function addMessage(messageContent, time) {
    const messageElement = document.createElement('div');
    messageElement.classList.add('message');
    messageElement.innerHTML = messageContent + `<span class="time">${time}</span>`;
    messagesContainer.appendChild(messageElement);
  }

  // Function to handle sending a message
  function sendMessage() {
    const message = inputMessage.value;
    if (message.trim() !== '') {
      const currentTime = new Date().toLocaleTimeString();
      addMessage(message, currentTime);
      inputMessage.value = '';
    } else {
      alert('请输入消息内容！');
    }
  }

  // Event listener for send button click
  sendButton.addEventListener('click', sendMessage);

  // Event listener for pressing enter key to send message
  inputMessage.addEventListener('keypress', function (e) {
    if (e.key === 'Enter') {
      sendMessage();
    }
  });
</script>

</body>
</html>
