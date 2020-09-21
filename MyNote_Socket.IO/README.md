# MyNote_Socket.IO

#### Index:

[Server-side Example](#Server-side) 

[In conjunction with Express](#In-conjunction-with-Express)

[Client-side](#Client-side)

___

### Server-side

https://github.com/socketio/socket.io 

Example:

```js
const server = require('http').createServer();
const io = require('socket.io')(server);
io.on('connection', client => {
    client.on('event', data => { /* … */ });
    client.on('disconnect', () => { /* … */ });
});
server.listen(3000);
```

### Step by step

```js
const http = require('http');
```

`'http'` 這個是 Node.js 的原生 module

```js
const server = require('http').createServer();
```

利用 `http` module 提供的 `createServer()` 去建立一個 http Server

`createServer()` 會返回一個新的 http.Server 實例

這裏有另一種寫法，`createServer()` 可以傳入一個含有兩個參數的 Lambda function :

```javascript
const server = require('http').createServer((request, response) => {
    // 處理 Client 向 http server 發送過來的 request
});
```

每當有 HTTP 請求到達服務器時，`createServer()` 中傳入的函數就會被自動執行。

事實上，這只是一種簡化寫法，以上等價：

```js
const server = require('http').createServer();
server.on('request', (request, response) => {
    // 處理 Client 向 http server 發送過來的 request
});
```

可以看看 [官方](https://nodejs.org/dist/latest-v4.x/docs/api/http.html#http_http_createserver_requestlistener) 的説明：

___

#### http.createServer([requestListener])

Returns a new instance of [`http.Server`](https://nodejs.org/dist/latest-v4.x/docs/api/http.html#http_class_http_server).

The `requestListener` is a function which is automatically added to the `'request'` event.

___

然後到 socket.io

```js
const io = require('socket.io')();
```

`'socket.io'` 不是 Node.js 的原生 module

所以你需要先安裝，例如用：`npm init -y    `  然後  `npm install socket.io`

___

`require('socket.io')`  返回了一個 `Server` Object 的 Constructor

所以上面的代碼等價：

```js
const io = require('socket.io')(); //上面的代碼
// 等價
const Server = require('socket.io');
const io = new Server();
```

這樣就獲取了一個 `Server` Object 的實例

看看 [官方](https://socket.io/docs/server-api/) 的説明，有三種 `Server` 的 Constructor:

#### new Server(httpServer[, options])

- `httpServer` *(http.Server)* the server to bind to.
- `options` *(Object)*

#### new Server(port[, options])

- `port` *(Number)* a port to listen to (a new `http.Server` will be created)
- `options` *(Object)*

#### new Server(options)

- `options` *(Object)*

See [above](https://socket.io/docs/server-api/#new-Server-httpServer-options) for the list of available `options`.

顯然由第一個 Constructor 可見，Socket.io 可以 using with http server:

```js
const server = require('http').createServer();
const io = require('socket.io')(server);
```

這就是 Example 頭兩行的意思

___

Socket.IO 允許你發送和接收自定義事件。除了 `connect`，`message` 和 `disconnect`。

有關 Socket.io 的 Events ，可以看 Stack Overflow 這個： [List of Socket.io Events](https://stackoverflow.com/questions/24224287/list-of-socket-io-events/24227414)

 Server-side 有 `connect` / `connection` event ，連接 Client 時觸發，connect 和 connection 這兩個是同義詞

我們可以用 `emit()` 和 `on()` 進行 event 的發送和監聽

```js
// emit() //
// 發送 event
.emit(eventName[, ...args]) 
.emit(<string> | <symbol>, <any>) // return <boolean>

// on() //
// 監聽 event 
.on(event, listener)
.on(<string> | <symbol>, <Function>) // return <EventEmitter>

// Event | Node.js v13.12.0 Documentation
// https://nodejs.org/api/events.html#events_emitter_emit_eventname_args
```

`connection` event 接收一個 `Socket`  ，即 `(socket) => { /* ... */ }`

`Socket` 有 `disconnect`, `error`, ... 等等 event 

回去看看 Example：

 ```js
const server = require('http').createServer();
const io = require('socket.io')(server);
io.on('connection', client => {
    client.on('event', data => { /* … */ });
    client.on('disconnect', () => { /* … */ });
});
server.listen(3000);
 ```

名爲 `io` 的  `Server` 實例 `.on()`  監聽 `connection` event

接收了 `Socket`，名爲 `client`

名爲 `client`的  `Socket`實例 `.on()` 監聽 `event` 和 `disconnect` event

最後 http server 監聽 3000 port

___

### In conjunction with Express

```js
const app = require('express')();
const server = require('http').createServer(app);
const io = require('socket.io')(server);
io.on('connection', () => { /* … */ });
server.listen(3000);
```

___

### Client-side

https://github.com/socketio/socket.io-client 

https://socket.io/docs/client-api/ 

```html
<script src="/socket.io/socket.io.js"></script>
<script>
  var socket = io('http://localhost');
  socket.on('connect', function(){});
  socket.on('event', function(data){});
  socket.on('disconnect', function(){});
</script>
```

