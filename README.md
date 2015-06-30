# 2015-node-chat-basic
=====================================
### 02. 정적 파일 서버 생성 
* 다음과 같이 디렉토리 생성 
<pre>
├── lib
└── public
    ├── javascripts
    └── stylesheets
</pre>

* server.js 파일 작성 
```javascript
var http = require('http');
var fs = require('fs');
var path = require('path');
var mime = require('mime');
var cache = {}; // 캐시
```


* 파일을 response 에 보내는 기능, 오류 response 전송 부분 작성
```javascript
function send404(response) {
  response.writeHead(404, {'Content-Type': 'text/plain'});
  response.write('Error 404: resource not found');
  response.end();
}

function sendFile(response, filePath, fileContents) {
  response.writeHead(200, {'Content-Type': mime.lookup(path.basename(filePath))});
  response.end(fileContents);
}
```

* 정적 파일 처리 부분 작성 
```javascript
function serveStatic(response, cache, absPath) {
  if (cache[absPath]) {
    sendFile(response, absPath, cache[absPath]);
  } else {
    fs.exists(absPath, function (exists) {
      if (exists) {
        fs.readFile(absPath, function (err, data) {
          if (err) {
            send404(response);
          } else {
            cache[absPath] = data;
            sendFile(response, absPath, data);
          }
        });
      } else {
        send404(response);
      }
    });
  }
}
```

* http 서버 생성, 시작 
```javascript
var server = http.createServer(function (request, response) {

  var filePath = false;
  if (request.url == '/') {
    filePath = 'public/index.html';
  } else {
    filePath = 'public' + request.url;
  }

  var absPath = './' + filePath;
  serveStatic(response, cache, absPath);
});

server.listen(3000, function () {
  console.log('Server listening in port 3000');
});
```

* 서버 시작 
```
$ node server.js
```

* 브라우저에서 확인 - 404 오류가 남
```
http://localhost:3000
```


