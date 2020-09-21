# MyNote_WebSocket

https://github.com/websockets/ws

https://github.com/websockets/ws/blob/master/doc/ws.md

___

```js
npm install ws
```

___

### Sending and receiving text data

```js
const WebSocket = require('ws');

const ws = new WebSocket('ws://www.host.com/path');

ws.on('open', () => {
  ws.send('something');
});

ws.on('message', (data) => {
  console.log(data);
});
```

[https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-%E8%AE%93%E5%89%8D%E5%BE%8C%E7%AB%AF%E6%B2%92%E6%9C%89%E8%B7%9D%E9%9B%A2-34536c333e1b](https://medium.com/enjoy-life-enjoy-coding/javascript-websocket-讓前後端沒有距離-34536c333e1b)

### Simple server

```js
const WebSocket = require('ws');

const wss = new WebSocket.Server({ port: 8080 });

wss.on('connection', (ws) => {
    
    ws.on('message', (message) => { /* ... */ });
    ws.on('close', () => { /* ... */ });

 	ws.send(/* ... */);
});
```

___

### Use with Express.js

```js
const app = require('express')();
const server = require('http').createServer(app);
const WebSocket = require('ws');
const wss = new WebSocket.Server({ server });

app.get('/', (req, res)=> {
    res.sendFile(/* ... */);
})

wss.on('connection', (ws) => {

    ws.on('message', (message) => { /* ... */ });
    ws.on('close', () => { /* ... */ });
        
});

server.listen(/* port */, () => {
    /* ... */
});
```

## Client-side

```html
<script>
    const ws = new WebSocket(`ws://${location.host}`);

    ws.onopen = function() { /* ... */ };
    ws.onmessage = function(event) { /* ... */ };
    ws.onclose = function() { /* ... */ };
</script>
```

https://www.runoob.com/html/html5-websocket.html

___

