# REPL

![Getting Started](./images/repl.png)

# CLI

```
const amount = 12;

if(amount<12){
    console.log('small no');
}else{
    console.log('large no');
}

```

![alt text](./images/cli.png)


# Global

```

//  Globals - No Winsdow

// global is a reference to the real global scope object in NodeJS,
//  somewhat like using window in a browser JS environment

console.log(__dirname);

setInterval(()=>{
  console.log("Hello World");
}, 1000)

```

# Modules

 `name.js`

```
const john ="John";
const peter = "Petere"
const secret = "Super Key"

module.exports = {john, peter}

```
`utils.js`

```
const sayHi = (name) =>{
    console.log(`Hello there ${name}`);
}

module.exports = sayHi

```

 `app.js`

```
// common js - Every File is module
//  Modules - Encapsulated code to share only minimum

const names = require('./name')
const sayHi = require('./utils')

sayHi(names.john);

```

## 1. OS Modules

```
const os = require('os');

// Info about current user

const user = os.userInfo();
console.log(user);

// Method return the system update 
console.log(`The system up time is ${os.uptime()} seconds`);

const currentOs = {
    name: os.type(),
    release: os.release(),
    totalMem: os.totalmem(),
    freeMem: os.freemem()
}

console.log(currentOs);

```

## 2. PATH Module

```
const path = require('path');

console.log(path.sep);

const filePath = path.join('/content/', 'subfolder', 'test.txt');

console.log(filePath);

const base = path.basename(filePath)

console.log(base);

```

## 3. FS Module

`FS Sync`

```
const {readFileSync, writeFileSync} = require('fs');

const first = readFileSync('./content/first.txt', 'utf8')
const second = readFileSync('./content/second.txt', 'utf8')

console.log(first);
console.log(second);

writeFileSync('./content/result.text', 'Here is the result')

```

`FS Async`

CallBack Hell

```
const {readFile, writeFile} = require('fs');

readFile('./content/first.txt', 'utf8', (err, result) =>{
    if(err){
        console.log(err);
        return
    }
    const first = result
    readFile('./content/second.txt', 'utf8', (err, result) =>{
        if(err){
            console.log(err);
            return
        }
        const second = result;

        writeFile('./content/result2.txt', `${first} ${second}`, (err, result) =>{
            if(err){
                return
                console.log(err);
            }
            console.log(result);
        });
    
    })
})

```
### Synx Vs Async

synchronous (sync) - you can only execute one thing at a time
asynchronous (async) - you can execute multiple things at the same time

## 4. HTTP Module

```
const http = require('http');

const server = http.createServer((req, res) =>{
    res.write("Welcome");
    res.end();
})

server.listen(5000);

```

# NPM

npm - global command comes with code.  
npm --v.  

local dependency - use it only in particular project.  
`npm i packageName`.  

global dependency - use it in any project.  
`npm i -g packageName`.  

package.json - manifest file.  
`npm init -y`.  

dev dependency- Not for production.  
`npm packageName -D`.  

## NPM Vs NPX
NPM is a package management that is used to install, uninstall, and update Javascript packages on your workstation.  
 whereas NPX is a package executer that is used to directly execute Javascript packages without installing them.

# Event Loop

[EventLoop Video](https://www.youtube.com/watch?v=8aGhZQkoFbQ).  

# Async Pattern

```
const http = require('http');
const server = http.createServer((req, res)=>{
 if(req.url === '/'){
    res.end('Home Page');
 }
 if(req.url === '/about'){
    // Blocking Code
    for (let i = 0; i < 1000; i++) {
        for (let j = 0; j < 1000; j++) {
           console.log("Hi");   
        }  
    }
    res.end('About Page');
 }
 res.end("Error");
})
server.listen(3000, () =>{
    console.log("Server Listening on port 3000");
})

```

```
const {readFile} = require('fs');

const getPath = (path) =>{
    return new Promise((res, rej) =>{
        readFile(path, 'utf8',(err, data) =>{
            if(err){
                rej(err);
            }else{
                res(data)
            }
        })
    })
}

getPath('../content/first.txt')
  .then((result) => console.log(result))
  .catch((err) => console.log(err));
```

# Events

Event-Driven Programming.  
used heavily in Node js.  

## Events Emitter

`Basic Setup`

```
const EventEmitter = require('events')

const coustomEmitter = new EventEmitter();

// on - listen an event
// emit - emit an event

coustomEmitter.on('response', () =>{
    console.log("Data fetched");
})

coustomEmitter.emit('response')

```
`Additional Info`

```
const EventEmitter = require('events')
const coustomEmitter = new EventEmitter();

// on - listen an event
// emit - emit an event
coustomEmitter.on('response', (name, age) =>{
    console.log(`Data fetched ${name} ${age}`);
})
coustomEmitter.on('response', () =>{
    console.log("Some other Logic");
})
// Logic will not broke If we use parameters

coustomEmitter.emit('response', 'John', 45)
```

# Streams

A stream is an abstract interface for working with streaming data in Node.js. The node:stream module provides an API for implementing the stream interface.  

There are many stream objects provided by Node.js. For instance, a request to an HTTP server and process.stdout are both stream instances.  

Streams can be readable, writable, or both. All streams are instances of EventEmitter.  


