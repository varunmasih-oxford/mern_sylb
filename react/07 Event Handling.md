# React Event Handling

## 1. What is Event Handling?

Event Handling in React allows components to respond to user actions.

Common user actions:

* Clicking buttons
* Typing in inputs
* Submitting forms
* Mouse movements

React events are similar to JavaScript events but follow **camelCase naming**.

Example:

```jsx
<button onClick={handleClick}>Click</button>
```

---

## 2. React Event Naming Rules

| HTML Event  | React Event |
| ----------- | ----------- |
| onclick     | onClick     |
| onchange    | onChange    |
| onsubmit    | onSubmit    |
| onmouseover | onMouseOver |

Rules:

* Use camelCase
* Pass function reference
* Do not call function directly

Correct:

```jsx
onClick={handleClick}
```

Wrong:

```jsx
onClick="handleClick()"
```

---

## 3. onClick Event

Triggered when a user clicks an element.

Example:

```jsx
function App() {

  const handleClick = () => {
    alert("Button Clicked");
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}

export default App;
```

---

## 4. onChange Event

Used with input fields.

Triggered when input value changes.

Example:

```jsx
import { useState } from "react";

function App() {

  const [name, setName] = useState("");

  const handleChange = (e) => {
    setName(e.target.value);
  };

  return (
    <div>
      <input
        type="text"
        onChange={handleChange}
      />
      <p>{name}</p>
    </div>
  );
}
```

---

## 5. onSubmit Event

Used with forms.

Example:

```jsx
function App() {

  const handleSubmit = (e) => {
    e.preventDefault();
    alert("Form Submitted");
  };

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

---

## 6. Passing Parameters in Events

Sometimes we need to pass data.

Example:

```jsx
function App() {

  const handleClick = (name) => {
    alert(name);
  };

  return (
    <button onClick={() => handleClick("Varun")}>
      Click
    </button>
  );
}
```

Explanation:

* Arrow function prevents automatic execution.

---

## 7. Event Object

React automatically provides an event object.

Example:

```jsx
const handleChange = (event) => {
  console.log(event.target.value);
};
```

Common properties:

* event.target
* event.target.value
* event.preventDefault()

---

## 8. Preventing Default Behavior

HTML forms refresh page by default.

React prevents this using:

```jsx
event.preventDefault();
```

Example:

```jsx
function App() {

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log("No Page Reload");
  };

  return (
    <form onSubmit={handleSubmit}>
      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

---

## 9. Multiple Events Example

```jsx
import { useState } from "react";

function App() {

  const [value, setValue] = useState("");

  const handleChange = (e) => {
    setValue(e.target.value);
  };

  const handleClick = () => {
    alert(value);
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input onChange={handleChange} />
      <button onClick={handleClick}>
        Show
      </button>
    </form>
  );
}
```

