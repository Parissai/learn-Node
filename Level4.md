## LEVEL 4 | Modules

|               custom_hello.js        |
|--------------------------------------|
```js
var hello = function(){
  console.log("hello!");
}

module.exports = hello;    //We can have only one module to export , only public method we could have    
```

|              custom_goodbye.js       |
|--------------------------------------|
```js
exports.goodbye = function() {	//We can have multiple public methods
	console.log('bye!');
}
```

|               app.js                 |
|--------------------------------------|
```js
var hello = require('./custom_hello');	
hello();

var gb = require('./custom_goodbye');		//Or  require('./custom_goodbye').goodbye();//if we only need to call once
gb.goodbye();
```
---
|             my_module.js             |
|--------------------------------------|
```js
var foo = function(){...}
var bar = function(){...}
var baz = function(){...}

exports.foo = foo;			//assigning it to the exports object.
exports.bar = bar;
```

|               app.js                 |
|--------------------------------------|
```js
var myMod = require('./my_module');
myMod.foo();
myMod.bar();
```
---

|          make_request.js             |
|--------------------------------------|
```js
var http = require('http');

var makeRequest = function(message) {
	
	var options = {
		host: 'localhost', port:8080, path: '/', method: 'Post'
	}

	var request = http.request(options, function(response){
		response.on('data', function(data){
			console.log(data);			//logs response body
		})
	})
	request.write(message); begins request
	request.end();
}

module.exports = makeRequest;
```


|               app.js                 |
|--------------------------------------|
```js
var makeRequest = require('./make_request');
makeRequest("Hello, this is dog.");
```
---
#### Installing a NPM module

```bash
$ npm install request
```
---
#### Making http request

```js
var http = require('http');
```
---
#### Install modules with executables globally

```bash
$ npm install coffee-script -g		//global
``` 	

```bash
$ coffee app.coffee			//local
```		
---

Global npm modules can't be required
```
$ npm install coffee-script -g
var coffee = require('coffee-script');	//X
```
```
$ npm install coffee-script   		//install them locally
var coffee = require('coffee-script');
```
Look for existing libraries here : [npm registry](https://www.npmjs.com/package/npm-registry)

---

{ "connect": "1.8.7"}

- 1  major version, will change
- 8  minor version, probably won't change
- 7  patch version, doesn't change the api


use the most recent tech so in package.json  use 

Ranges	
- "connect": "~1"  => most recent between 1.0.0 and 2.0.0	//Dangerous
- "connect": "~1.8"  => most recent between 1.8.0 and 1.9.0	//API could change
- "connect": "~1.8.7"  => most recent between 1.8.7 and 1.9.0	//Considered safe

for semantic versioning  http://semver.org

---

