# Node.js File System (fs)

# 1. What is the File System (fs) Module?

The **fs module** allows Node.js to interact with the file system on your computer.

It is used for:

* Reading files
* Creating files
* Writing data
* Updating files
* Deleting files

The `fs` module is a **built-in Node.js module**, so you do not need to install it.

Import it like this:

```js
const fs = require("fs")
```

---

# 2. Reading Files

The `readFile()` method is used to read the content of a file.

Syntax:

```js
fs.readFile(path, encoding, callback)
```

Example:

```js
const fs = require("fs")

fs.readFile("test.txt", "utf8", (err, data) => {

  if (err) {
    console.log(err)
    return
  }

  console.log(data)

})
```

Explanation:

* `"test.txt"` → file name
* `"utf8"` → encoding
* `err` → error if file not found
* `data` → file content

---

# 3. Writing Files

The `writeFile()` method creates a new file or overwrites an existing file.

Syntax:

```js
fs.writeFile(path, data, callback)
```

Example:

```js
const fs = require("fs")

fs.writeFile("test.txt", "Hello Node.js", (err) => {

  if (err) {
    console.log(err)
    return
  }

  console.log("File created successfully")

})
```

Important:

* If the file already exists → content will be replaced.

---

# 4. Appending Data to Files

The `appendFile()` method adds content to an existing file.

Syntax:

```js
fs.appendFile(path, data, callback)
```

Example:

```js
const fs = require("fs")

fs.appendFile("test.txt", "\nNew line added", (err) => {

  if (err) {
    console.log(err)
    return
  }

  console.log("Data appended successfully")

})
```

Difference from `writeFile`:

* `writeFile()` replaces content
* `appendFile()` adds content

---

# 5. Deleting Files

The `unlink()` method deletes a file.

Syntax:

```js
fs.unlink(path, callback)
```

Example:

```js
const fs = require("fs")

fs.unlink("test.txt", (err) => {

  if (err) {
    console.log(err)
    return
  }

  console.log("File deleted successfully")

})
```

---

# 6. Creating Files

Files can also be created using `writeFile`.

Example:

```js
const fs = require("fs")

fs.writeFile("newFile.txt", "New file created", (err) => {

  if (err) {
    console.log(err)
    return
  }

  console.log("File created")

})
```

---

# 7. Complete Example

```js
const fs = require("fs")

// Create file
fs.writeFile("example.txt", "Hello", (err) => {
  if (err) throw err
  console.log("File created")
})

// Append data
fs.appendFile("example.txt", "\nWelcome to Node", (err) => {
  if (err) throw err
  console.log("Data added")
})

// Read file
fs.readFile("example.txt", "utf8", (err, data) => {
  if (err) throw err
  console.log(data)
})

// Delete file
fs.unlink("example.txt", (err) => {
  if (err) throw err
  console.log("File deleted")
})
```

---

# 8. Asynchronous vs Synchronous

Node.js provides two versions.

### Asynchronous (Recommended)

```js
fs.readFile("test.txt","utf8",(err,data)=>{
 console.log(data)
})
```

Non-blocking.

---

### Synchronous

```js
const data = fs.readFileSync("test.txt","utf8")
console.log(data)
```

Blocks the execution.

