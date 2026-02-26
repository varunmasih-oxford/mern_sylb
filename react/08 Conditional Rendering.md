# React Conditional Rendering

## 1. What is Conditional Rendering?

Conditional Rendering in React means displaying UI elements based on conditions.

React decides **what to show** depending on:

* User login status
* Data availability
* Role permissions
* User actions

Example:

* Show Dashboard if user logged in
* Show Login page if not logged in

---

## 2. Using if/else Logic

Used when conditions are complex.

Example:

```jsx
function App() {

  const isLoggedIn = true;

  if (isLoggedIn) {
    return <h1>Welcome User</h1>;
  } else {
    return <h1>Please Login</h1>;
  }
}

export default App;
```

---

## 3. Conditional Rendering Inside Component

Using variable before return.

```jsx
function App() {

  const isAdmin = false;
  let message;

  if (isAdmin) {
    message = "Admin Panel";
  } else {
    message = "User Panel";
  }

  return <h1>{message}</h1>;
}
```

---

## 4. Ternary Operator

Short syntax for if/else.

Syntax:

```jsx
condition ? trueValue : falseValue
```

Example:

```jsx
function App() {

  const isLoggedIn = true;

  return (
    <div>
      {isLoggedIn ? <h1>Dashboard</h1> : <h1>Login</h1>}
    </div>
  );
}
```

Use when:

* Two possible outputs exist.

---

## 5. Logical AND Operator (&&)

Used when rendering something **only if condition is true**.

Syntax:

```jsx
condition && component
```

Example:

```jsx
function App() {

  const showMessage = true;

  return (
    <div>
      {showMessage && <h2>Hello User</h2>}
    </div>
  );
}
```

If condition is false → nothing renders.

Use when:

* No else condition needed.

---

## 6. Showing and Hiding Components

Example using state:

```jsx
import { useState } from "react";

function App() {

  const [show, setShow] = useState(false);

  return (
    <div>

      <button onClick={() => setShow(!show)}>
        Toggle
      </button>

      {show && <h2>Component Visible</h2>}

    </div>
  );
}
```

---

## 7. Rendering Different Components

Example:

```jsx
function Login() {
  return <h2>Login Page</h2>;
}

function Dashboard() {
  return <h2>Dashboard</h2>;
}

function App() {

  const isLoggedIn = true;

  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
  );
}
```

---

## 8. Multiple Conditions

Example:

```jsx
function App() {

  const role = "admin";

  return (
    <div>
      {role === "admin"
        ? "Admin Panel"
        : role === "trainer"
        ? "Trainer Panel"
        : "Student Panel"}
    </div>
  );
}
```

