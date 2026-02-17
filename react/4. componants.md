# 04 - Components in React
---

# 1. What are Components?

A component is a reusable piece of UI in React.

Think of components like small building blocks:
- Header
- Footer
- Navbar
- Card
- Button
- Form

React applications are built by combining multiple components together.

---

# 2. Functional Components

Modern React uses **Functional Components**.

A functional component is simply a JavaScript function that returns JSX.

## Basic Example

```jsx
function Welcome() {
  return <h1>Welcome to React</h1>;
}

export default Welcome;
````

## Using the Component

```jsx
import Welcome from "./Welcome";

function App() {
  return (
    <div>
      <Welcome />
    </div>
  );
}

export default App;
```

---

# 3. Step-by-Step: Create Your First Component

## Step 1: Create a New File

Inside the `src` folder, create:

```
Header.jsx
```

## Step 2: Write Functional Component

```jsx
function Header() {
  return <h2>This is Header Component</h2>;
}

export default Header;
```

## Step 3: Use It Inside App.jsx

```jsx
import Header from "./Header";

function App() {
  return (
    <div>
      <Header />
    </div>
  );
}

export default App;
```

Save and check browser.

---

# 4. Component Naming Rules

React components must follow these rules:

## Rule 1: First Letter Must Be Capital

Correct:

```jsx
function Header() {}
```

Incorrect:

```jsx
function header() {}
```

Reason:
React treats lowercase names as normal HTML tags.

---

## Rule 2: Use PascalCase

PascalCase means every word starts with a capital letter.

Correct:

* UserCard
* ProductList
* LoginForm

Incorrect:

* userCard
* product_list
* login-form

---

## Rule 3: One Component Per File (Best Practice)

Each file should usually contain one component.

Example:

```
Header.jsx
Footer.jsx
Navbar.jsx
```

---

# 5. Creating Reusable Components

Reusable components can be used multiple times with different data.

## Example: Card Component

Create:

```
Card.jsx
```

```jsx
function Card(props) {
  return (
    <div>
      <h3>{props.title}</h3>
      <p>{props.description}</p>
    </div>
  );
}

export default Card;
```

Use in `App.jsx`:

```jsx
import Card from "./Card";

function App() {
  return (
    <div>
      <Card title="React" description="Frontend Library" />
      <Card title="Node" description="Backend Runtime" />
    </div>
  );
}

export default App;
```

Now the same component is reused with different data.

---

# 6. Making Components More Clean (Destructuring Props)

Instead of:

```jsx
function Card(props) {
  return <h3>{props.title}</h3>;
}
```

Use:

```jsx
function Card({ title, description }) {
  return (
    <div>
      <h3>{title}</h3>
      <p>{description}</p>
    </div>
  );
}
```

This makes the component cleaner.

---

# 7. Organizing Components (Project Structure)

As your project grows, organize components properly.

## Small Project Structure

```
src/
 ├── App.jsx
 ├── Header.jsx
 ├── Footer.jsx
 ├── Card.jsx
```

---

## Medium Project Structure (Recommended)

Create a folder:

```
src/
 ├── components/
 │     ├── Header.jsx
 │     ├── Footer.jsx
 │     ├── Card.jsx
 ├── App.jsx
 ├── main.jsx
```

Import like this:

```jsx
import Header from "./components/Header";
```

---

## Large Project Structure (Feature-Based)

```
src/
 ├── components/
 ├── pages/
 ├── layouts/
 ├── hooks/
 ├── App.jsx
```

* components → reusable UI parts
* pages → full pages (Home, About)
* layouts → structure (Navbar + Footer)
* hooks → custom hooks

---
