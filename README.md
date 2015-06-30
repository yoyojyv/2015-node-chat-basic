# 2015-node-chat-basic
=====================================
### 03. 정적 파일 서버 생성2 
* html 파일, css 파일 추가 

* index.html
```html
<!doctype html>
<html lang='en'>

<head>
  <title>Chat</title>
  <link rel='stylesheet' href='/stylesheets/style.css'></link>
</head>

<body>
<div id='content'>
  <div id='room'></div>
  <div id='room-list'></div>
  <div id='messages'></div>

  <form id='send-form'>
    <input id='send-message' />
    <input id='send-button' type='submit' value='Send'/>

    <div id='help'>
      Chat commands:
      <ul>
        <li>Change nickname: <code>/nick [username]</code></li>
        <li>Join/create room: <code>/join [room name]</code></li>
      </ul>
    </div>
  </form>
</div>

<script src='/socket.io/socket.io.js' type='text/javascript'></script>
<script src='http://code.jquery.com/jquery-1.8.0.min.js' type='text/javascript'></script>
<script src='/javascripts/chat.js' type='text/javascript'></script>
<script src='/javascripts/chat_ui.js' type='text/javascript'></script>
</body>
</html>
```

* style.css 추가 
```css
body {
  padding: 50px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}

a {
  color: #00B7FF;
}

#content {
  width: 800px;
  margin-left: auto;
  margin-right: auto;
}

#room {
  background-color: #ddd;
  margin-bottom: 1em;
}

#messages {
  width: 690px;
  height: 300px;
  overflow: auto;
  background-color: #eee;
  margin-bottom: 1em;
  margin-right: 10px;
}

#room-list {
  float: right;
  width: 100px;
  height: 300px;
  overflow: auto;
}

#room-list div {
  border-bottom: 1px solid #eee;
}

#room-list div:hover {
  background-color: #ddd;
}

#send-message {
  width: 600px;
  margin-bottom: 1em;
  margin-right: 1em;
}

#help {
  font: 10px "Lucida Grande", Helvetica, Arial, sans-serif;
}
```
