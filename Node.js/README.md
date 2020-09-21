# MyNote_Node.js

#### Index

[Get command line arguments](#Get-command-line-arguments)

[fs, File System](#fs-File-System) 

[child_process, Chid Process](#child_process-Chid-Process)

[net, Net](#net-Net)

[dns, DNS](#dns-DNS)

[os, OS](#os-OS)

[Timers](#Timers)

___

### Get command line arguments 

https://nodejs.org/docs/latest/api/process.html#process_process_argv 

```js
process.argv // return <string[]>
```

Example:

```js
node test.js one two 

// [0]: /usr/local/bin/node 
// [1]: /Users/test.js
// [2]: one
// [3]: two
```

[0] is `process.execPath`   http://nodejs.cn/api/process.html#process_process_execpath 

[1] is location of exec file

___

### fs, File System

https://nodejs.org/api/fs.html#fs_file_system

___

### child_process, Chid Process

https://nodejs.org/api/child_process.html#child_process_child_process

___

### net, Net

https://nodejs.org/api/net.html#net_net

https://www.runoob.com/nodejs/nodejs-net-module.html 

```js
net.createServer([options][, connectionListener])

// Sample 1 //
const net = require('net');
const server = net.createServer((c) => {
	// 'connection' listener.
    console.log('client connected');
    c.on('end', () => {
    	console.log('client disconnected');
    });
    c.write('hello\r\n');
    c.pipe(c);
});
server.on('error', (err) => {
    throw err;
});
server.listen(8124, () => {
    console.log('server bound');
});

// Sample 2 //
const net = require('net');
net.createServer( connection => { // connection is `net.Socket`
    connection.write(/* ... */);
    connection.on('lookup',  () => { /* ... */ });
    connection.on('connect', () => { /* ... */ });
    connection.on('data',    () => { /* ... */ });
    connection.on('end',     () => { /* ... */ });
    connection.on('timeout', () => { /* ... */ });
    connection.on('close',   () => { /* ... */ });
    connection.on('error',   (err) => { /* ... */ });
    // ...
}).listen(8124, () => { /* ... */ });
```

Creates a new TCP or IPC server.

https://nodejs.org/api/net.html#net_net_createserver_options_connectionlistener

___

### dns, DNS

https://nodejs.org/api/dns.html

https://www.runoob.com/nodejs/nodejs-dns-module.html

```js
dns.lookup(hostname[, options], callback)

//callback
(err, address, family) => { /* ... */ }
```

https://nodejs.org/api/dns.html#dns_dns_lookup_hostname_options_callback

___

### os, OS

https://nodejs.org/api/os.html

https://www.runoob.com/nodejs/nodejs-os-module.html

```js
os.hostname() // return <string>
```

https://nodejs.org/api/os.html#os_os_hostname

___

### Timers

https://nodejs.org/api/timers.html

https://nodejs.org/zh-cn/docs/guides/timers-in-node/

```js
setInterval(callback, delay[, ...args]) // return <Timeout>

// callback
() => { /* ... */ }
```

___



