# JWT Practice Project (Node.js + Express + MongoDB)

# 1. Create Project Folder

Open terminal and run:

```bash
mkdir jwt-practice
cd jwt-practice
```

Initialize Node project:

```bash
npm init -y
```

Project now:

```
jwt-practice
 └── package.json
```

---

# 2. Install Required Packages

```bash
npm install express mongoose jsonwebtoken bcryptjs dotenv cors
```

Optional (for development):

```bash
npm install nodemon --save-dev
```

---

# 3. Create Folder Structure

Inside the project folder create these folders:

```bash
mkdir models
mkdir routes
mkdir middleware
```

Project structure:

```
jwt-practice
│
├── models
├── routes
├── middleware
└── package.json
```

---

# 4. Create Main Server File

Create file in the **root folder**:

```
server.js
```

Structure now:

```
jwt-practice
│
├── models
├── routes
├── middleware
├── server.js
└── package.json
```

---

# 5. Create Environment File

Create a file in the **root folder**:

```
.env
```

Add the following:

```
MONGO_URL=mongodb://127.0.0.1:27017/jwtpractice
JWT_SECRET=mysecretkey
```

Structure:

```
jwt-practice
│
├── models
├── routes
├── middleware
├── server.js
├── .env
└── package.json
```

---

# 6. Create User Model

Create file:

```
models/User.js
```

Example code:

```javascript
const mongoose = require("mongoose")

const userSchema = new mongoose.Schema({
  name: String,
  email: String,
  password: String
})

module.exports = mongoose.model("User", userSchema)
```

---

# 7. Create Authentication Routes

Create file:

```
routes/authRoutes.js
```

This file will contain:

- Register API
- Login API
- Protected route

Basic structure:

```javascript
const express = require("express")
const router = express.Router()

router.get("/", (req,res)=>{
  res.send("Auth Routes Working")
})

module.exports = router
```

---

# 8. Create JWT Middleware

Create file:

```
middleware/auth.js
```

Example middleware:

```javascript
const jwt = require("jsonwebtoken")

function auth(req,res,next){

  const token = req.headers.authorization

  if(!token){
    return res.json({message:"Access Denied"})
  }

  try{

    const verified = jwt.verify(token,process.env.JWT_SECRET)
    req.user = verified
    next()

  }catch(err){
    res.json({message:"Invalid Token"})
  }

}

module.exports = auth
```

---

# 9. Setup Express Server

Add the following code in:

```
server.js
```

```javascript
const express = require("express")
const mongoose = require("mongoose")
require("dotenv").config()

const authRoutes = require("./routes/authRoutes")

const app = express()

app.use(express.json())

mongoose.connect(process.env.MONGO_URL)
.then(()=>console.log("MongoDB Connected"))
.catch(err=>console.log(err))

app.use("/api",authRoutes)

app.listen(5000,()=>{
  console.log("Server running on port 5000")
})
```

---

# 10. Final Project Structure

Your project should look like this:

```
jwt-practice
│
├── models
│   └── User.js
│
├── routes
│   └── authRoutes.js
│
├── middleware
│   └── auth.js
│
├── server.js
├── .env
├── package.json
└── node_modules
```

---

# 11. Run the Server

Start the server:

```bash
node server.js
```

or

```bash
npx nodemon server.js
```

Server runs on:

```
http://localhost:5000
```

---

# 12. APIs to Test (Postman)

### Register User

```
POST /api/register
```

Example body:

```json
{
"name":"Varun",
"email":"varun@test.com",
"password":"123456"
}
```

---

### Login User

```
POST /api/login
```

Response:

```
{
 "token":"JWT_TOKEN"
}
```

---

### Access Protected Route

```
GET /api/profile
```

Header:

```
Authorization: JWT_TOKEN
```

---

# 13. JWT Authentication Flow

```
User Register
      ↓
Password Hashed (bcrypt)
      ↓
User Login
      ↓
Server Generates JWT Token
      ↓
Client Stores Token
      ↓
Client Sends Token in Header
      ↓
Server Verifies Token (Middleware)
      ↓
Access Protected Routes
```

---

