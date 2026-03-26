## Core Terms

* **Socket.IO** → Library for real-time communication
* **Node.js** → Server environment to run Socket.IO
* **Client** → Browser or frontend app
* **Server** → Backend handling connections

---

## Connection Terms

* **Connection** → When a client connects to server
* **Socket** → Unique connection instance for each user
* **Socket ID** → Unique identifier of each connected client
* **Disconnect** → When user leaves or loses connection

---

## Communication Terms

* **Event** → Named message (e.g., "chat message")
* **emit()** → Send event/data
* **on()** → Listen/receive event
* **Message** → Data sent between client & server

---

## Broadcasting Terms

* **io.emit()** → Send to all clients
* **socket.emit()** → Send to specific client
* **socket.broadcast.emit()** → Send to all except sender

---

## Grouping Terms

* **Room** → Group of sockets (e.g., chat room)
* **join()** → Add user to room
* **leave()** → Remove user from room
* **io.to(room).emit()** → Send message to specific room

---

## Structure Terms

* **Namespace** → Separate communication channel (e.g., `/chat`)
* **Default Namespace (`/`)** → Main connection path

---

## Transport & Tech Terms

* **WebSocket** → Fast real-time protocol
* **HTTP Polling** → Backup when WebSocket fails
* **Handshake** → Initial connection setup

---

## Development Terms

* **Server Instance (`io`)** → Main Socket.IO server object
* **Client Instance (`socket`)** → Client connection object
* **Listener** → Function waiting for event
* **Callback** → Function executed after event

---

# Socket.IO working

---

## Step 1: Create Project

```bash
mkdir socket-minimal
cd socket-minimal
npm init -y
````

---

## Step 2: Install Packages

```bash
npm install express socket.io
```

---

## Step 3: Create `server.js`

```javascript
const express = require("express");
const http = require("http");
const { Server } = require("socket.io");

const app = express();
const server = http.createServer(app);
const io = new Server(server);

// Serve HTML file
app.get("/", (req, res) => {
  res.sendFile(__dirname + "/index.html");
});

// Socket connection
io.on("connection", (socket) => {
  console.log("User connected");

  socket.on("message", (msg) => {
    io.emit("message", msg);
  });
});

server.listen(3000, () => {
  console.log("http://localhost:3000");
});
```

---

## Step 4: Create `index.html`

```html
<!DOCTYPE html>
<html>
<head>
  <title>Socket.IO</title>
</head>
<body>

<input id="msg" placeholder="Type message" />
<button onclick="send()">Send</button>

<ul id="list"></ul>

<script src="/socket.io/socket.io.js"></script>

<script>
  const socket = io();

  function send() {
    const msg = document.getElementById("msg").value;
    socket.emit("message", msg);
  }

  socket.on("message", (msg) => {
    const li = document.createElement("li");
    li.textContent = msg;
    document.getElementById("list").appendChild(li);
  });
</script>

</body>
</html>
```

---

## Step 5: Run Server

```bash
node server.js
```

Open browser:

```
http://localhost:3000
```

---

## Step 6: Test

* Open multiple tabs
* Send message from one tab
* Message appears in all tabs instantly

---

## How It Works

1. Client connects using `io()`
2. Server listens using `connection`
3. Client sends message using `emit()`
4. Server broadcasts using `io.emit()`
5. Clients receive using `on()`

