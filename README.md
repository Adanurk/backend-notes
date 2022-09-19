# Backend Notes
NodeJs, Express &amp; MongoDB Bootcamp notes.

## Part 1: Node.JS Basics

### Section 1: Introduction

- code along
- coding challenges
- take notes
- Q & A

### Section 2: Introduction to Node.js and NPM

+ Node.js => a js runtime built on googles open source v8 js engine.
+ so we can run our code outside of browser.
+ v8 engine run the code.
+ so we can access to file sytem with nodejs. We couldnt do that on browser.

=> so it is perfect to use Node.js as a web server
=> meaning: we can finally use js on the server side of the web development in order to build fast highly scalable network applications.

**pros**
+ single threaded, event driven, non blocking
+ perfect for building fast and scalable data intensive apps
+ many good companies use node.js (netflix, uber, paypal)
+ same language full stack - so it is fast and efficient
+ huge library of open source packages (NPM)
+ very active developer community

**use for**
+ API with databasem(preferably NoSQL)
+ data streaming
+ real time chat app
+ server side web apps

**not good for**
+ apps with super heavy server side processing, file compression etc => for these php, python, rails

**Notes:**
+ you can use ES6 or older, any JS will work.Because we dont run js on browser, but on server. We running it inside node app.
+ write node on terminal, it starts node, when you hit tab it shows u all global variables.
+ "_" it means your previous result!
+ String. + tab => shows u all related methods/constructors and so on

**Modules**
+ all kinds of additional functionality are stored in module.
+ reading files ability is inside fs module.
```JavaScript
const fs = require("fs");
```
+ so we get address to functions related with file system
+ we call it with require and it returns an object with functions
+ and we stored this object into fs variable
+ so we can use it later

[Node Documentation](https://nodejs.org/en/docs/)

```JavaScript
const textIn = fs.readFileSync("./txt/input.txt", "utf-8");
//syncronous way of file reading there is also async version
//two arguments => path to file, and second one character encoding(usually utf-8)
console.log(textIn);

fs.writeFileSync("./txt/output.txt", textOut);
//first argument is path, second one the thing we want to write
```
**sync - async code**

+ processing one by one, each one waits the result of previous one
+ so it is blocking code
+ this is a problem
+ as solution used async nonblocking codes
+ in async, we have a callback funtion to handle the result when the process is done
+ so the codes are not blocked by the heavy tasks run in the background

```JavaScript
const fs = require("fs");
fs.readFile("input.txt", "utf-8", (err, data) => {
  console.log(data);
 });
 console.log("Reading file...");
 //first it sees readFile, it is async code, so while it is processes in the background it goes down and prints reading file and then data.
 + here the third argument our function takes is a callback to process result when it is ready.
 ```
 + single thread: there is only one signle thread. the thread is where our code actually executed in machines processor. All the users using same thread.
 + always same place for all users. So one user need to wait others to go on.
 + so async code we use for dealing with heavy work in the background! Time consuming tasks should be executed here.
 + non blocking I/O model => input output
 + this is why we use so many callback functions in Node.js / for example in php it is very different concept!
 + callbacks are not automatically async!
 + the problem is callback hell! nested callbacks can be very confusing. this triangular shape is a sign that you are in a callback hell.
 + how can we escape callback hell? => using promises or async / await (more elegant way)
 
 **note**: arrow function doesnt have its own this keyword, uses the parents this keyword / lexical scope we call it. normal function has its own scope, own this keyword.
 
 **Creating a simple web server**
 
 + we need another package calles http. IT gives us networking capability.
 
 
```JavaScript
const server = http.createServer((req, res) => {
    // console.log(req);
    res.end("Hello from the server!")
});
// server is the result ot createSERver method
// createServer takes a callback function, will be fired each time a request to a server,
//this callback has access to fundamental variables, request and response variable.
//each time the server gets request, this response will be called,
//these two are objects, inside we have useful tools to deal with request and response
//.end is the simplest way to send a simple response

server.listen(8000, "127.0.0.1", () => {
    console.log("Listening to requests on port 8000");
})

//local host simply means the current computer, "127.0.0.1" is the standard IP address for it.
//due to event loop, it(server that we created) doesnt exits from app, 
//because the whole goal is the waiting for requests, this is the point about server
//when we write http://127.0.0.1:8000/ to the browser we see the response from server
 ```
 
 **Routing**
 
 + host/port/urlname
 + implementing different actions for different url => routing
 + for routing we need "url" modul.
 ```JavaScript
 const url = require("url");
 ```
 + browser automatically request for websites icon (fav icon)
 + http header => is  a piece of info we are sending back from server
 + we can use it to send some metadata for errors:
  ```JavaScript
const server = http.createServer((req, res) => {
    const pathName =  req.url;
    if(pathName === "/" || pathName === "/overview"){
        res.end("This is the overview")
    }else if(pathName === "/product"){
        res.end("This is the product")
    }else{
        res.writeHead(404, {
            "Content-type" : "text/html",
            "my-own-header":"hello-world"
        });
        res.end("<h1>Page not found</h1>")
    }
});
 ```
 
 **API**
 
 + a service from which you can request some data.
 + JSON is a very simple text format similar to JS format.
 + using dirname variable is better practice instead of using . (dot) for the current directory in the paths inside methods.
 + because usually . (dot) means where your script is working and __dir means where the current file is located.
 => __dirname is path of the directory that contains current file ( the file inside which you are writing __dirname)
 => ./ refers to the path of directory where terminal is opened.
 ```JavaScript
 else if(pathName === "/api"){
        fs.readFile(`${__dirname}/dev-data/data.json`, ...)
        res.end("API");
 ```
 + one exception about meaning / usage of dot is : require function! 
 + JSON.parse() => parse() The JSON. parse() method parses a JSON string, constructing the JavaScript value or object described by the string. Parses into an object.
 + sync / top-level code only executes once but async code / callback will executed each time there is a request!
 + it is important to understand which code will executed once in the beginning and which one will executed again and again.
 ```JavaScript
 const data = fs.readFileSync(`${__dirname}/dev-data/data.json`, "utf-8");
const dataObj = JSON.parse(data);
//parses this into an object

const server = http.createServer((req, res) => {
    const pathName =  req.url;
    if(pathName === "/" || pathName === "/overview"){
        res.end("This is the overview");
    }else if(pathName === "/product"){
        res.end("This is the product");
    }else if(pathName === "/api"){
            res.writeHead(200, {"Content-type": "application/json"});
            res.end(data);
    }else{
        res.writeHead(404, {
            "Content-type" : "text/html",
            "my-own-header":"hello-world"
        });
        res.end("<h1>Page not found</h1>")
    }
});
```

+ use reqular expressions instead of quotes here, because it only replaces first one if you use quotes. but regular expressions with /g replaces all.
```JavaScript
const replaceTemplate = (temp, product) => {
    let output = temp.replace(/{%PRODUCTNAME}/g, product.productName)
}
```

**difference between import and require:** The major difference between require and import, is that require will automatically scan node_modules to find modules, but import, which comes from ES6, won't.

![foto1](./img/import-vs-require.png)
 

## Part 2: How Node Works

### Section 3: Introduction to Back-End Web Development

### Section 4: How Node.js Works: A Look Behind the Scenes

## Optional Part

### Section 5: Asynchronous JavaScript: Promises and Async/Await

## Part 3: "Natours" API

### Section 6: Express: Starting Building the Natours API

### Section 7: Introduction to MongoDB

### Section 8: Mongoose

### Section 9: Error Handling with Express

### Section 10: Authentication, Authorization and Security

### Section 11: Modelling Data and Advanced Mongoose

## Part 4: "Natours" Site

### Section 12: Server-Side Rendering with Pug Templates

### Section 13: Advanced Features: Payments, Email, File Uploads

### Section 14: Setting Up Git and Deployment

### Last Notes
