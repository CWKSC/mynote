# MyNote_Express.js

```javascript
var express = require('express')
var app = express()
```

#### app.get(path, callback [, callback ...])

Routes HTTP GET requests to the specified path with the specified callback functions.

```javascript
app.get('/', function (req, res) {
    /* ... */
})
```

#### res.sendFile(path [, options] [, fn])

```js
app.get('/', (req, res) => {
    res.sendFile(/* ... */);
})
```

#### get, post, put, delete

```js
// https://ithelp.ithome.com.tw/articles/10185811

var express = require('express');
var app = express();

app.get('/', function (req, res) {
    res.send("<html><body><h1>Hello World</h1></body></html>");
});
 
app.post('/submit-data', function (req, res) {
    res.send('POST Request');
});
 
app.put('/update-data', function (req, res) {
    res.send('PUT Request');
});
 
app.delete('/delete-data', function (req, res) {
    res.send('DELETE Request');
});
 
var server = app.listen(5000, function () {
    console.log('Node server is running..');
});
```

