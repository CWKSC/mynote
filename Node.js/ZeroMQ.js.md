# MyNote_ZeroMQ.js

https://github.com/zeromq/zeromq.js

http://zeromq.github.io/zeromq.js/ 

https://zeromq.org/languages/nodejs/

___

```js
$ npm install zeromq@5
```

___

```js
const zmq = require("zeromq")
```

___

### Messaging Patterns

1. Publisher / Subscriber
2. Request / Reply
3. Router / Dealer
4. Pushing / Pulling

### Publisher / Subscriber

Publisher send message to all Subscriber

Publisher can't receive message

Subscribe can't send message

http://zguide.zeromq.org/js:wuserver

```js
// Weather update server in node.js
// Binds PUB socket to tcp://*:5556
// Publishes random weather updates

var zmq = require('zeromq')
  , publisher = zmq.socket('pub');

publisher.bindSync("tcp://*:5556");
publisher.bindSync("ipc://weather.ipc");

function zeropad(num) {
  return num.toString().padStart(5, "0");
};

function rand(upper, extra) {
  var num = Math.abs(Math.round(Math.random() * upper));
  return num + (extra || 0);
};

while (true) {
  // Get values that will fool the boss
  var zipcode     = rand(100000)
    , temperature = rand(215, -80)
    , relhumidity = rand(50, 10)
    , update      = `${zeropad(zipcode)} ${temperature} ${relhumidity}`;
  publisher.send(update);
}
```

### Request / Reply

when server get request (message), reply (message)

one request for mult reply need polling, it will process one by one

http://zguide.zeromq.org/js:hwserver

```js
var zmq = require('zmq');

// socket to talk to clients
var responder = zmq.socket('rep');

responder.on('message', function(request) {
    console.log("Received request: [", request.toString(), "]");

    // do some 'work'
    setTimeout(function() {
        // send reply back to client.
        responder.send("World");
    }, 1000);
});

responder.bind('tcp://*:5555', function(err) {
  if (err) { console.log(err);
  } else { console.log("Listening on 5555…"); }
});

process.on('SIGINT', function() {
  responder.close();
});
```

### Router / Dealer

http://zguide.zeromq.org/page:all#advanced-request-reply

Advance of Request / Reply 

income message(Request) send to router, router send to dealer

dealer have some worker to work

when dealer get request form router, dealer will send to worker

worker finish the work and reply to dealer

dealer forward to router, router reply to correspond request.

http://zguide.zeromq.org/js:rrbroker

```js
// Simple request-reply broker in Node.js

var zmq      = require('zmq')
  , frontend = zmq.socket('router')
  , backend  = zmq.socket('dealer');

frontend.bindSync('tcp://*:5559');
backend.bindSync('tcp://*:5560');

frontend.on('message', function() {
  // Note that separate message parts come as function arguments.
  var args = Array.apply(null, arguments);
  // Pass array of strings/buffers to send multipart messages.
  backend.send(args);
});

backend.on('message', function() {
  var args = Array.apply(null, arguments);
  frontend.send(args);
});
```

### Pushing / Pulling

Similar to Publisher and Subscriber

Pusher push one message, then only one puller get the message

### bi-directional Pushing and Pulling

use cluster https://nodejs.org/api/cluster.html#cluster_cluster 

```js
const cluster = require('cluster');
const numCPUs = require('os').cpus().length;
if (cluster.isMaster) {
    /* ... */
}else{
    /* ... */
}
```

The master cluster create pusher and puller

pusher use to push task to worker cluster

puller use to pull result from worker cluster

and also reponsible to fork worker cluster

Form worker clusters:

worker clusters create pusher and puller

puller use to pull task from masker cluster

pusher use to push result to masker cluster

```js
const zmq = require('zmq');
const cluster = require('cluster');
const numCPUs = require('os').cpus().length;
if (cluster.isMaster) {
    
    const masterPusher = zmq.socket('push');
    masterPusher.bind(/* ... */);
    masterPusher.send(/* ... */); // call worker
    
    const masterPuller = zmq.socket('pull');
    masterPuller.bind(/* ... */);
    masterPuller.on('message', msg => {
        /* get the result */
    });
    
    for (let i = 0; i < numCPUs; i++) {
        cluster.fork();
    }
    
}else{
    
    const workerPusher = zmq.socket('push').connect(/* ... */);
    const workerPuller = zmq.socket('pull').connect(/* ... */);
    
    workerPuller.on('message', msg => {
        // Do work 
        workerPusher.send(/* work result */);
    });
}
```



___

官方 Sample

### Push/Pull

```js
// producer.js
var zmq = require("zeromq"),
sock = zmq.socket("push");

sock.bindSync("tcp://127.0.0.1:3000");
console.log("Producer bound to port 3000");

setInterval(function() {
  console.log("sending work");
  sock.send("some work");
}, 500);
```

```js
// worker.js
var zmq = require("zeromq"),
  sock = zmq.socket("pull");

sock.connect("tcp://127.0.0.1:3000");
console.log("Worker connected to port 3000");

sock.on("message", function(msg) {
  console.log("work: %s", msg.toString());
});
```

### Pub/Sub

```js
// pubber.js
var zmq = require("zeromq"),
  sock = zmq.socket("pub");

sock.bindSync("tcp://127.0.0.1:3000");
console.log("Publisher bound to port 3000");

setInterval(function() {
  console.log("sending a multipart message envelope");
  sock.send(["kitty cats", "meow!"]);
}, 500);
```

```js
// subber.js
var zmq = require("zeromq"),
  sock = zmq.socket("sub");

sock.connect("tcp://127.0.0.1:3000");
sock.subscribe("kitty cats");
console.log("Subscriber connected to port 3000");

sock.on("message", function(topic, message) {
  console.log(
    "received a message related to:",
    topic,
    "containing message:",
    message
  );
});
```

### other example

```js
const zmq = require('zeromq');

const publisher = zmq.socket('pub');
publisher.bind("tcp://*:" + port, err =>{
    if(err) throw err;
    /* ... */
})

const responder = zmq.socket('rep');
responder.bind("tcp://127.0.0.1:" + port, err => {
    if(err) throw err;
    /* ... */
})

responder.on('message', data =>{
    /* ... */
    // publisher.send(/* ... */);
    // responder.send(/* ... */);
})
```

```js
const zmq = require('zeromq');
const pushSocket = zmq.socket('push');

pushSocket.bind("tcp://*:" + port, err =>{
    if(err) throw err;
    /* ... */
    // pushSocket.send(/* ... */);
})
```

```js
const zmq = require('zeromq');
const pullSocket = zmq.socket('pull');

pullSocket.on('message', msg => {
    /* ... */
})

pullSocket.connect('tcp://127.0.0.1:' + port);
```

