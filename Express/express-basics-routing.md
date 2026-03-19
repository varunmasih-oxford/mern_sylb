# Express.js Basics + Routing


# 1. Setup Project

Create a new folder:

```bash
mkdir express-basics
cd express-basics
```

Initialize Node project:

```bash
npm init -y
```

Install Express:

```bash
npm install express
```

---

# 2. Create First Server

Create file in root folder:

```
server.js
```

Add code:

```javascript
const express = require("express")
const app = express()

app.listen(3000, () => {
  console.log("Server running on port 3000")
})
```

Run server:

```bash
node server.js
```

Open browser:

```
http://localhost:3000
```

---

# 3. Create First Route (GET)

Update `server.js`:

```javascript
app.get("/", (req, res) => {
  res.send("Welcome to Express Server")
})
```

---

# 4. Multiple Routes

```javascript
app.get("/about", (req, res) => {
  res.send("About Page")
})

app.get("/contact", (req, res) => {
  res.send("Contact Page")
})
```

Test:

```
/about
/contact
```

---

# 5. HTTP Methods

### GET

```javascript
app.get("/users", (req, res) => {
  res.send("Get all users")
})
```

### POST

```javascript
app.post("/users", (req, res) => {
  res.send("User created")
})
```

### PUT

```javascript
app.put("/users", (req, res) => {
  res.send("User updated")
})
```

### DELETE

```javascript
app.delete("/users", (req, res) => {
  res.send("User deleted")
})
```

---

# 6. Route Parameters

```javascript
app.get("/user/:id", (req, res) => {
  res.send(`User ID is ${req.params.id}`)
})
```

Example:

```
http://localhost:3000/user/101
```

---

# 7. Multiple Parameters

```javascript
app.get("/user/:id/:name", (req, res) => {
  res.send(`ID: ${req.params.id}, Name: ${req.params.name}`)
})
```

---

# 8. Query Parameters

```javascript
app.get("/search", (req, res) => {
  res.send(`Search keyword: ${req.query.q}`)
})
```

Example:

```
http://localhost:3000/search?q=nodejs
```

---

# 9. Sending JSON Response

```javascript
app.get("/api/users", (req, res) => {
  res.json([
    { id: 1, name: "Varun" },
    { id: 2, name: "Rahul" }
  ])
})
```

---

# 10. Status Codes

```javascript
app.get("/error", (req, res) => {
  res.status(404).send("Page not found")
})
```

---

# 11. Route Chaining

```javascript
app.route("/product")
  .get((req, res) => {
    res.send("Get Products")
  })
  .post((req, res) => {
    res.send("Add Product")
  })
```

---

# 12. Organizing Routes (Router)

Create folder:

```
routes/
```

Create file:

```
routes/userRoutes.js
```

Add:

```javascript
const express = require("express")
const router = express.Router()

router.get("/", (req, res) => {
  res.send("All Users")
})

module.exports = router
```

Use in `server.js`:

```javascript
const userRoutes = require("./routes/userRoutes")

app.use("/users", userRoutes)
```

Test:

```
http://localhost:3000/users
```

---

# Final Project Structure

```
express-basics
│
├── routes
│   └── userRoutes.js
│
├── server.js
├── package.json
└── node_modules
```

---

# Practice Tasks

1. Create routes:
   - `/home`
   - `/services`
   - `/blog`

2. Create dynamic route:
   - `/product/:id`

3. Create API:
   - `/api/products` (return JSON)

4. Create query route:
   - `/filter?category=mobile`

5. Create route with multiple params:
   - `/order/:id/:status`

---

# What You Learned

- Express setup  
- Server creation  
- Routing basics  
- HTTP methods  
- Route parameters  
- Query parameters  
- JSON responses  
- Route organization  

---
