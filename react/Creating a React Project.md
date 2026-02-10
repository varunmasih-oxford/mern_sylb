# Creating a React Project

---

## 1. Install Node.js

React requires Node.js to run.

1. Visit: https://nodejs.org  
2. Download the **LTS (Long Term Support)** version  
3. Install it  
4. Verify installation:

```bash
node -v
npm -v
````

Both commands should display version numbers.

---

## 2. Create a React Project (Using Vite)

Vite is fast and modern.

```bash
npm create vite@latest
```

Answer the prompts:

| Question     | Select       |
| ------------ | ------------ |
| Project name | my-react-app |
| Framework    | React        |
| Variant      | JavaScript   |

---

## 3. Open Project Folder

```bash
cd my-react-app
```

---

## 4. Install Dependencies

```bash
npm install
```

---

## 5. Start Development Server

```bash
npm run dev
```

Open the shown local URL (usually [http://localhost:5173](http://localhost:5173)) in your browser.

---

## 6. Understand Project Structure

| File/Folder  | Purpose            |
| ------------ | ------------------ |
| node_modules | Installed packages |
| public       | Static files       |
| src          | Main source code   |
| src/main.jsx | Entry point        |
| src/App.jsx  | Main component     |
| index.html   | Root HTML file     |

---

## 7. Clean Default Code

Open **src/App.jsx** and replace with:

```jsx
function App() {
  return (
    <div>
      <h1>My First React App</h1>
    </div>
  );
}

export default App;
```

---

## 8. Create Your First Component

Create **src/Header.jsx**

```jsx
function Header() {
  return <h2>Welcome to React</h2>;
}

export default Header;
```

Use it in **App.jsx**

```jsx
import Header from "./Header";

function App() {
  return (
    <div>
      <Header />
      <p>This is my React project.</p>
    </div>
  );
}

export default App;
```

---

## 9. Using Props

**Header.jsx**

```jsx
function Header(props) {
  return <h2>Hello, {props.name}</h2>;
}

export default Header;
```

**App.jsx**

```jsx
<Header name="Varun" />
```

---

## 10. Adding State with useState

```jsx
import { useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h1>Counter App</h1>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}

export default App;
```

---

## 11. Handling Events

```jsx
<button onClick={() => alert("Button Clicked!")}>
  Click Me
</button>
```

Common events:

* onClick
* onChange
* onSubmit
* onMouseOver

---

## 12. Working with Forms

```jsx
import { useState } from "react";

function App() {
  const [name, setName] = useState("");

  return (
    <div>
      <input 
        type="text" 
        placeholder="Enter name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <p>Hello {name}</p>
    </div>
  );
}

export default App;
```

---

## 13. Styling in React

### CSS File Method

Create **src/App.css**

```css
body {
  font-family: Arial;
}
h1 {
  color: blue;
}
```

Import in **App.jsx**

```jsx
import "./App.css";
```

### Inline Styling

```jsx
<h1 style={{ color: "red" }}>Styled Text</h1>
```

---

## 14. Multiple Components

Create **src/Footer.jsx**

```jsx
function Footer() {
  return <p>Copyright 2026</p>;
}

export default Footer;
```

Use in **App.jsx**

```jsx
import Footer from "./Footer";

<Footer />
```

---

## 15. React Router (Multiple Pages)

Install router:

```bash
npm install react-router-dom
```

**main.jsx**

```jsx
import { BrowserRouter } from "react-router-dom";
import App from "./App";

<BrowserRouter>
  <App />
</BrowserRouter>
```

**App.jsx**

```jsx
import { Routes, Route, Link } from "react-router-dom";

function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}

function App() {
  return (
    <div>
      <nav>
        <Link to="/">Home</Link> | <Link to="/about">About</Link>
      </nav>

      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </div>
  );
}

export default App;
```

---

## 16. Build for Production

```bash
npm run build
```

Creates a **dist** folder with optimized files.

---

## 17. Preview Production Build

```bash
npm run preview
```

---

## 18. Deploy Your React App

You can deploy using:

* Netlify
* Vercel
* GitHub Pages
* Firebase Hosting

Upload the **dist** folder to host your app.

---
