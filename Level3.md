LEVEL 3 | Streams

Can be READABLE(request),	WRITABLE (response) or  BOTH

---
```
http.createServer(function(request, response){
	response.writeHead(200);
	response.write("<p>Dog is running.</p>");
	setTimeout(function(){
		response.write("<p>Dog is done</p>");
		response.end();
	}, 5000);

}).listen(8080);
```
---
```
http.creatServer(function(request, response){
	response.writeHead(200);
	request.on('readable', function(){
		var chunk = null;
		while (null !== (chunk = request.read())){
			response.write(chunk);	//console.log(chunk.toString());
		}
	})
	request.on('end', function(){
		response.end();
	});
}).listen(8080);
```
---

### PIPE THESE TWO TOGETHER 
```
request.on('readable', function(){
	var chunk = null;
	while (null !== (chunk = request.read())){
		response.write(chunk);	//console.log(chunk.toString());
	}
})
request.on('end', function(){
	response.end();
});
```
====
```request.pipe(response);``` 

SO 
```
http.creatServer(function(request, response){
	response.writeHead(200);
	request.pipe(response);
}).listen(8080);
```
And with ```$ curl -d 'hello' http://localhost:8080```       //Hello on client
PIPE OUTPUT OF THE FIRST FUNCTION = INPUT OF SECOND FUNCTION

---
```
var fs = require('fs');	//require filesystem module

var file = fs.createReadStream('readme.md');
var newFile = fs.createWriteStream('readme_copy.md');

file.pipe(newFile);
```
---
```
var fs = require('fs');
var http = require('http');

http.createServer(function(request, response){
	var newFile = fs.createWriteStream("readme_copy.md");
	request.pipe(newFile);

	request.on('end', function(){
		respond.end('uploaded!');
	});
}).listen(8080);
```
```$ curl --upload-file readme.md http://localhost:8080```
---

### UPLOADING A FILE
```
http.createServer(function(request, response){
	var newFile = fs.createWriteStream("readme_copy.md");
	var fileBytes = request.headers['content-length'];
	var uploadedBytes = 0;
	request.on('readable', function(){
		var chunk = null;
		while(null !== (chunk = request.read())){
			uploadedBytes += chunk.length;
			var progress = (uploadesdBytes / fileBytes) * 100;
			response.write("progress: " + parseInt(progress, 10) + "%\n");
		}
	});
	request.pipe(newFile);
	...
}).listen(8080);
```
```$ node app.js	//Listening on port 8080
$ curl --upload-file large_file.jpg http://localhost:8080
1%
2%
.....
```


---

### Exercises

#### File Read Stream

```var fs = require('fs');
var file = fs.createReadStream('fruits.txt');

file.on('readable', function(){
  var chunk = null;
  while(null !== (chunk = file.read())){
    console.log(chunk.toString());    
  }  
});
```
---

#### File Piping

```var fs = require('fs');

var file = fs.createReadStream('fruits.txt');
file.pipe(process.stdout);
```
---

#### Fixing Pipe

```var fs = require('fs');

var file = fs.createReadStream('origin.txt');
var destFile = fs.createWriteStream('destination.txt');

file.pipe(destFile, { end: false });	//second argument prevents pipe from closing automatically our 

writable stream.

file.on('end', function(){
  destFile.end('Finished!');
});
```
