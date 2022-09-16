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
