# Student Profiling System

## Project Features

* Add Student Profile (Create)
* View All Students (Read)
* Update Student Details (Update)
* Delete Student (Delete)
* Upload Profile Image
* REST API with MongoDB
* React Frontend

---

## Step 1: Project Setup

### Create Root Folder

```bash
mkdir student-profiling-system
cd student-profiling-system
```

### Create Backend & Frontend

```bash
mkdir backend
mkdir frontend
```

---

## Step 2: Backend Setup (Node + Express)

### Initialize Backend

```bash
cd backend
npm init -y
```

### Install Packages

```bash
npm install express mongoose cors multer dotenv
npm install nodemon --save-dev
```

---

## Folder Structure

```
backend/
│-- models/
│-- routes/
│-- uploads/
│-- server.js
│-- .env
```

---

## Create Server (server.js)

```js
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");
require("dotenv").config();

const app = express();

app.use(cors());
app.use(express.json());
app.use("/uploads", express.static("uploads"));

mongoose.connect(process.env.MONGO_URI)
.then(() => console.log("MongoDB Connected"))
.catch(err => console.log(err));

app.use("/api/students", require("./routes/studentRoutes"));

app.listen(5000, () => console.log("Server running on port 5000"));
```

---

## MongoDB Connection (.env)

```
MONGO_URI=mongodb://127.0.0.1:27017/studentDB
```

---

## Step 3: Create Model

### models/Student.js

```js
const mongoose = require("mongoose");

const studentSchema = new mongoose.Schema({
    name: String,
    studentId: String,
    course: String,
    mobile: String,
    image: String
});

module.exports = mongoose.model("Student", studentSchema);
```

---

## Step 4: CRUD Routes

### routes/studentRoutes.js

```js
const express = require("express");
const router = express.Router();
const Student = require("../models/Student");
const multer = require("multer");

const storage = multer.diskStorage({
    destination: "uploads/",
    filename: (req, file, cb) => {
        cb(null, Date.now() + "-" + file.originalname);
    }
});

const upload = multer({ storage });

// CREATE
router.post("/", upload.single("image"), async (req, res) => {
    try {
        const newStudent = new Student({
            ...req.body,
            image: req.file.filename
        });
        await newStudent.save();
        res.json(newStudent);
    } catch (err) {
        res.status(500).json(err);
    }
});

// READ
router.get("/", async (req, res) => {
    const students = await Student.find();
    res.json(students);
});

// UPDATE
router.put("/:id", async (req, res) => {
    const updated = await Student.findByIdAndUpdate(req.params.id, req.body, { new: true });
    res.json(updated);
});

// DELETE
router.delete("/:id", async (req, res) => {
    await Student.findByIdAndDelete(req.params.id);
    res.json({ message: "Deleted" });
});

module.exports = router;
```

---

## Run Backend

```bash
npx nodemon server.js
```

---

## Step 5: Frontend Setup (React)

### Create React App

```bash
cd ../frontend
npx create-react-app .
npm install axios
```

---

## Folder Structure

```
src/
│-- components/
│   │-- AddStudent.js
│   │-- StudentList.js
│-- App.js
```

---

## Step 6: Add Student Form

### components/AddStudent.js

```jsx
import React, { useState } from "react";
import axios from "axios";

function AddStudent() {
  const [form, setForm] = useState({
    name: "",
    studentId: "",
    course: "",
    mobile: ""
  });
  const [image, setImage] = useState(null);

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    const data = new FormData();
    Object.keys(form).forEach(key => data.append(key, form[key]));
    data.append("image", image);

    await axios.post("http://localhost:5000/api/students", data);
    alert("Student Added");
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name" placeholder="Name" onChange={handleChange} />
      <input name="studentId" placeholder="ID" onChange={handleChange} />
      <input name="course" placeholder="Course" onChange={handleChange} />
      <input name="mobile" placeholder="Mobile" onChange={handleChange} />
      <input type="file" onChange={(e) => setImage(e.target.files[0])} />
      <button>Add Student</button>
    </form>
  );
}

export default AddStudent;
```

---

## Step 7: Display Students

### components/StudentList.js

```jsx
import React, { useEffect, useState } from "react";
import axios from "axios";

function StudentList() {
  const [students, setStudents] = useState([]);

  const fetchStudents = async () => {
    const res = await axios.get("http://localhost:5000/api/students");
    setStudents(res.data);
  };

  useEffect(() => {
    fetchStudents();
  }, []);

  const deleteStudent = async (id) => {
    await axios.delete(`http://localhost:5000/api/students/${id}`);
    fetchStudents();
  };

  return (
    <div>
      {students.map(s => (
        <div key={s._id}>
          <img src={`http://localhost:5000/uploads/${s.image}`} width="100" />
          <h3>{s.name}</h3>
          <p>{s.course}</p>
          <button onClick={() => deleteStudent(s._id)}>Delete</button>
        </div>
      ))}
    </div>
  );
}

export default StudentList;
```

---

## Step 8: Connect Components

### App.js

```jsx
import AddStudent from "./components/AddStudent";
import StudentList from "./components/StudentList";

function App() {
  return (
    <div>
      <h1>Student Profiling System</h1>
      <AddStudent />
      <StudentList />
    </div>
  );
}

export default App;
```

---

## Run Frontend

```bash
npm start
```

---
