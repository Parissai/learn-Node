## LEVEL 4 | Modules

|               custom_hello.js        |
|--------------------------------------|
```
var hello = function(){
  console.log("hello!");
}

module.exports = hello;    //We can have only one module to export , only public method we could have    
```

|              custom_goodbye.js       |
|--------------------------------------|
```
exports.goodbye = function() {	//We can have multiple public methods
	console.log('bye!');
}
```

|               app.js                 |
|--------------------------------------|
```
var hello = require('./custom_hello');	
hello();

	
var gb = require('./custom_goodbye');		//Or  require('./custom_goodbye').goodbye();//if we only need to call once
gb.goodbye();
```
---
|             my_module.js             |
|--------------------------------------|
```
var foo = function(){...}
var bar = function(){...}
var baz = function(){...}

exports.foo = foo;			//assigning it to the exports object.
exports.bar = bar;
```

|               app.js                 |
|--------------------------------------|
```
var myMod = require('./my_module');
myMod.foo();
myMod.bar();
```
---






