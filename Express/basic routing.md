
# 1. Route Parameters

### What it means:

Route parameters are **dynamic values in the URL path**.

* Defined using `:`
* Accessed using `req.params`

### Code:

```js
app.get("/user/:id", (req, res) => {
  res.send(`User ID is ${req.params.id}`)
})
```

### Example:

```
http://localhost:3000/user/101
```

### Output:

```
User ID is 101
```

### Explanation:

* `/user/:id` → `:id` is dynamic
* `101` → stored in `req.params.id`

---

# 2. Multiple Route Parameters

### What it means:

You can pass multiple values in the URL.

### Code:

```js
app.get("/user/:id/:name", (req, res) => {
  res.send(`ID: ${req.params.id}, Name: ${req.params.name}`)
})
```

### Example:

```
http://localhost:3000/user/101/varun
```

### Output:

```
ID: 101, Name: varun
```

### Explanation:

* `:id` → 101
* `:name` → varun
* Both values are accessed using `req.params`

---

# 3. Query Parameters

### What it means:

Query parameters are used to send optional data in the URL after `?`

### Format:

```
?key=value
```

### Code:

```js
app.get("/search", (req, res) => {
  res.send(`Search keyword: ${req.query.q}`)
})
```

### Example:

```
http://localhost:3000/search?q=nodejs
```

### Output:

```
Search keyword: nodejs
```

### Explanation:

* `q=nodejs` → key = `q`, value = `nodejs`
* Access using `req.query.q`

---

# 4. Sending JSON Response

### What it means:

Send structured data (JSON) instead of plain text.

### Code:

```js
app.get("/api/users", (req, res) => {
  res.json([
    { id: 1, name: "Varun" },
    { id: 2, name: "Rahul" }
  ])
})
```

### Output:

```json
[
  { "id": 1, "name": "Varun" },
  { "id": 2, "name": "Rahul" }
]
```

### Explanation:

* Used in APIs
* Easy to use in frontend applications

---

# 5. Status Codes

### What it means:

Status codes tell the client what happened with the request.

### Code:

```js
app.get("/error", (req, res) => {
  res.status(404).send("Page not found")
})
```

### Output:

```
Page not found
```

### Common Status Codes:

| Code | Meaning      |
| ---- | ------------ |
| 200  | OK (Success) |
| 201  | Created      |
| 400  | Bad Request  |
| 401  | Unauthorized |
| 404  | Not Found    |
| 500  | Server Error |

---

# Final Summary

| Concept         | Used For            | Access Method |
| --------------- | ------------------- | ------------- |
| Route Params    | Required URL values | req.params    |
| Multiple Params | Multiple values     | req.params    |
| Query Params    | Optional data       | req.query     |
| JSON Response   | Send data           | res.json()    |
| Status Codes    | Response status     | res.status()  |

