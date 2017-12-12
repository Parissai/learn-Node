## LEVEL 2 | Events

### Custom event emitter

```
var EventEmitter = require('events').EventEmitter;
var logger = new EventEmitter();		//error  warn   info

logger.on('error', function(message) {
	console.log('ERR: ' + message);
});

logger.emit('error', 'Spilled Milk');
logger.emit('error', 'Eggs raked');
```

### Create server

```http.createServer(function(request, response) {...});```    //create with parameters
###### OR
```var server = http.createServer();```		//create without parameters

```server.on('request', function(request, response){...});```	//you could listen to multiple event listener this way or have multiple function to listen to the same event

---

### Exercises

#### Chat Emitter

```
var events = require('events');
var EventEmitter = events.EventEmitter;
var chat = new EventEmitter();
chat.on('message', function(message){
  console.log(message);
});
```
---
#### Request Event

```
var http = require('http');

var server = http.createServer();
server.on('request', function(request, response) {
  response.writeHead(200);
  response.write("Hello, this is dog");
  response.end();
});

server.on('request', function(request, response){
  console.log("New request coming in...");
});

server.listen(8080);
```
