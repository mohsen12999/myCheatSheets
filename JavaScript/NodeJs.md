# Node

a runtime enviroment for executing Javascript code.
to make Highly-scalable, data-intensive and real-time app.

- Great for prototyping and agile development.
- superfast and highly scalable.
- Javacript everywhere.
- cleaner and more consist codebase.
- largest ecosystem of open-source libs

- Node is NOT a programming language! and its not a framework.
- Non-blocking: Asynchronous
- add all request in Event Queue
- Node is ideal for I/O-intensive app -> more request
- Do note use for CPU-intensive app -> like video incoding or image proccess
- Node is c++ app for run javascript with v8 engine (chrome javascript engine)

## install Node

download from [nodejs site](https://nodejs.org/en/)

`node -v` or `node --version`

`npm -v`

`npm install -g npm@latest`

## make first app

make `app.js`

```js
function sayHello(name) {
  console.log("Hello " + name);
}

sayHello("Mohsen");
```

`node app.js`

## Node Modules

- os, fs, events, http

## Global Object

- setTimeout(), clearInterval(), setInterval(), clearInterval()
- not window or document
- varible are only valid in scope (file) and member of `module` variable

## Create Module

make logger.js

```js
var url = "http://mylogger.io/log";
function log(message) {
  // Send an HTTP request
  console.log(message);
}
module.exports.log = log;
module.exports.endPoint = url; // difference name
```

- if we have only one export object

```js
module.exports = log;
```

## Load Module

```js
const logger = require("./logger"); // better use const vs var for probably change
logger.log("message");
```

- `jshint app.js` -> show error in better way

## Module Wrapper Function

node add function like that to module

```js
(function (exports, require, module, __filename, __direname) {
  //module command here
});
```

## Modules

go to [nodejs doc](https://nodejs.org/en/docs/) -> click on your version api on left side -> can see built-in module

usefull module: File System, HTTP, OS, Path, Process, Querry Strings, Stream, ...

### Path Module

- path.parse(path)

```js
const path = require("path");
var pathObj = path.parse(__filename);
console.log(pathObj);
```

os -> os.userInfo([options])

```js
const os = require("os");
var totalMemory = os.totalmem();
var freeMemory = os.freemem();
console.log("Total Memory: " + totalMemory);
// use template string (ES6)
console.log(`Free Memory: ${freeMemory}`);
```

### filesystem Module

```js
const fs = require("fs"); // have sync or async method
//sync method -> dont use in real world app
const files = fs.readdirSync("./");
console.log(files);
//async metod
fs.readdir("./", function (err, files) {
  if (err) console.log("Error", err);
  else console.log("Result", files);
});
```

### Events Module

EventEmitter

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();
//emmit.addListener -> for Register a listener
emmit.on("messageLogged", function () {
  console.log("Listener Called");
});
// event must regester before emit
emitter.emit("messageLogged"); // for rase an event, make a noise, product signal for event
```

- event arguments -> pass data to event

```js
const EventEmitter = require("events");
const emitter = new EventEmitter();
// ES6 arrow function
emmit.on("messageLogged", (arg) => {
  console.log("Listener Called", arg);
});
emitter.emit("messageLogged", { id: 1, url: "http://" });
```

```js
const EventEmitter = require("events");
// ES6
class Logger extends EventEmitter {
  log(message) {
    console.log("Listener Called");
    this.emmit("messageLogged", { id: 1, url: "http://" });
  }
}
module.export = Logger;
```

```js
const EventEmitter = require("events");

const Logger = require("./logger");
const logger = new Logger();

logger.on("messageLogged", (arg) => {
  console.log("Listener Called", arg);
});

logger.log("message");
```

### HTTP Module

```js
const http = require("http");
const server = http.creatServer((req, res) => {
  if (req.url === "/") {
    res.write("Hello World!");
    res.end();
  }
  if (req.url === "/api/courses") {
    res.write(JSON.stringify([1, 2, 3]));
    res.end();
  }
});
// server.on('connection', (socket) => {
//     console.log('new connection');
// })
server.listen(3000);
console.log("Listen on Port 3000");
```

## update node

[update link](https://nodejs.org/en/download/package-manager/)

## make node project

`node init` -> make project.json file

## install requirement or update

`npm install` or `npm i`

## more

https://hasura.io/
https://nestjs.com/
https://www.prisma.io/
http://knexjs.org/
https://jestjs.io/
https://Cypress.io
