## LEVEL 1 | Intro to Node.js

|               hello.js        |
|-------------------------------|
```
var http = require('http');	//how we require modules

http.createServer(function(request, response){
	response.writeHead(200);	//Status code in header
	response.write("Hello, this is a dog.");		//Response body
	response.end();		//close the connecttion
}).listen(8080);		//listen for connection on this port

console.log('Listening on port 8080...');
```
```
$ node hello.js	//Run the server	
$ curl http://localhost:8080 
```
---
```
var fs = require('fs');

fs.readFile('index.html', function(error, contents){
  console.log(contents);
});
```
---
```
var http = require('http');
var fs = require('fs');

http.createServer(function(request, response) {
  response.writeHead(200, {
  'Content-Type': 'text/html' });

  fs.readFile('index.html', function(err, contents) {
    response.write(contents);
    response.end();
  });

}).listen(8080);
```