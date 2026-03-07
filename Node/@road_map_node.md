# 1. Node.js Fundamentals

Understand the basics of how Node.js works.

Topics to learn:

* What is Node.js
* Node.js vs Browser JavaScript
* Event-driven architecture
* Non-blocking I/O
* Single-threaded event loop
* Global objects

Important globals:

```js
console.log(__dirname)
console.log(__filename)
console.log(process.version)
```

---

# 2. Node.js Modules System

Node uses modules to organize code.

Topics:

* CommonJS modules
* `require()`
* `module.exports`
* ES Modules (`import` / `export`)

Example:

```js
// math.js
function add(a, b) {
  return a + b
}

module.exports = add
```

```js
// app.js
const add = require("./math")

console.log(add(2,3))
```

---

# 3. Core Node Modules

Node provides built-in modules.

Important modules:

### File System (fs)

Used for file operations.

* read files
* write files
* append files
* delete files

Example:

```js
const fs = require("fs")

fs.readFile("test.txt","utf8",(err,data)=>{
  console.log(data)
})
```

---

### Path Module

Used for handling file paths.

```js
const path = require("path")

console.log(path.join(__dirname,"file.txt"))
```

---

### OS Module

Used to get system information.

```js
const os = require("os")

console.log(os.platform())
```

---

### HTTP Module

Used to create servers.

```js
const http = require("http")

const server = http.createServer((req,res)=>{
  res.end("Server running")
})

server.listen(3000)
```

---

# 4. NPM (Node Package Manager)

NPM is used to install packages.

Important concepts:

* package.json
* dependencies
* scripts
* installing libraries

Commands:

```bash
npm init -y
npm install express
npm install nodemon --save-dev
```

---

# 5. Express.js

Express is the most popular Node.js framework.

Topics to learn:

* Creating server
* Routing
* Middleware
* Request and Response
* REST APIs

Example:

```js
const express = require("express")

const app = express()

app.get("/",(req,res)=>{
  res.send("Hello World")
})

app.listen(3000)
```

---

# 6. REST API Development

Learn how to build APIs.

HTTP Methods:

* GET
* POST
* PUT
* DELETE

Example:

```js
app.get("/users",(req,res)=>{
  res.json({message:"Users List"})
})
```

---

# 7. Middleware

Middleware functions run during the request cycle.

Example:

```js
app.use((req,res,next)=>{
  console.log("Request received")
  next()
})
```

Types:

* Built-in middleware
* Custom middleware
* Third-party middleware

---

# 8. Database Integration

Learn at least one database.

Recommended:

MongoDB with Mongoose

Topics:

* Database connection
* Schema
* Models
* CRUD operations

Example:

```js
const mongoose = require("mongoose")

mongoose.connect("mongodb://localhost:27017/app")
```

---

# 9. Authentication Basics

Learn basic authentication system.

Topics:

* Login system
* Password hashing
* JWT Authentication
* Protected routes

Libraries:

* bcrypt
* jsonwebtoken

---

# 10. Environment Variables

Used to store secrets and configuration.

Use `.env` file.

Example:

```
PORT=5000
DB_URL=mongodb://localhost:27017/app
JWT_SECRET=secretkey
```

Access in code:

```js
process.env.PORT
```

---

# 11. Asynchronous Programming

Node.js relies heavily on asynchronous code.

Topics:

* Callbacks
* Promises
* async/await
* Error handling

Example:

```js
async function getData(){
  const data = await fetchData()
  console.log(data)
}
```

---

# 12. Error Handling

Handle errors properly in APIs.

Example:

```js
try {
  const data = await User.find()
} catch(error){
  console.log(error)
}
```

Express error middleware:

```js
app.use((err,req,res,next)=>{
  res.status(500).json({error:err.message})
})
```

---

# 13. Project Structure

A basic backend project structure:

```
project/
│
├── routes/
├── controllers/
├── models/
├── middleware/
├── config/
├── server.js
```

---

# 14. Testing APIs

Tools used for testing APIs:

* Postman
* Thunder Client

Learn to test:

* GET requests
* POST requests
* Authorization headers
* JSON responses

---

# 15. Deployment Basics

Learn how to run applications in production.

Basic topics:

* Environment configuration
* Running server in production
* Hosting Node.js apps

Popular platforms:

* Render
* Railway
* VPS servers

---

# Recommended Learning Order

1. Node.js Fundamentals
2. Modules System
3. Core Modules
4. NPM
5. Express.js
6. REST APIs
7. Middleware
8. MongoDB / Database
9. Authentication (JWT)
10. Deployment

---

# Minimum Full Stack Path

React → Node.js → Express → MongoDB → JWT

This stack is called **MERN Stack**.

---
