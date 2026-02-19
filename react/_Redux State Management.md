# Redux State Management

---

# 1. What is Redux?

Redux is a state management library used to manage global state in large React applications.

It provides:
- Centralized state management
- Predictable state updates
- Better debugging

Redux is useful when multiple components need access to the same data.

---

# 2. Why Redux?

Problems in large applications:

- Prop drilling
- Complex state logic
- Difficult debugging
- Shared state across many components

Redux solves this by creating a single global store.

---

# 3. Core Concepts of Redux

Redux has 3 main parts:

1. Store
2. Action
3. Reducer

---

## 3.1 Store

The Store holds the entire application state.

Think of it as a global JavaScript object.

---

## 3.2 Action

An action is a plain JavaScript object that describes what happened.

Example:

```js
{
  type: "INCREMENT"
}
````

---

## 3.3 Reducer

A reducer is a function that:

* Takes current state
* Takes action
* Returns new state

Example:

```js
function counterReducer(state = { count: 0 }, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
}
```

---

# 4. Redux Data Flow

Redux follows one-way data flow:

Component → Dispatch Action → Reducer → Store → UI Update

Steps:

1. User clicks button
2. Action dispatched
3. Reducer updates state
4. Store updates
5. Component re-renders

---

# 5. Modern Redux (Redux Toolkit)

Redux Toolkit is the recommended way to use Redux.

Install:

```bash
npm install @reduxjs/toolkit react-redux
```

---

# 6. Step-by-Step Counter Example (Redux Toolkit)

---

## Step 1: Create Redux Folder

Create inside `src`:

```
redux/
```

---

## Step 2: Create Store

Create `store.js`

```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer
  }
});
```

---

## Step 3: Create Slice

Create `counterSlice.js`

```js
import { createSlice } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { count: 0 },
  reducers: {
    increment: (state) => {
      state.count += 1;
    },
    decrement: (state) => {
      state.count -= 1;
    }
  }
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

---

## Step 4: Connect Store to React

Open `main.jsx`

```jsx
import React from "react";
import ReactDOM from "react-dom/client";
import App from "./App";
import { Provider } from "react-redux";
import { store } from "./redux/store";

ReactDOM.createRoot(document.getElementById("root")).render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

---

## Step 5: Use Redux in Component

Open `App.jsx`

```jsx
import { useSelector, useDispatch } from "react-redux";
import { increment, decrement } from "./redux/counterSlice";

function App() {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <div>
      <h1>Redux Counter</h1>
      <h2>{count}</h2>
      <button onClick={() => dispatch(increment())}>Increase</button>
      <button onClick={() => dispatch(decrement())}>Decrease</button>
    </div>
  );
}

export default App;
```

---

# 7. Important Redux Hooks

## useSelector

Used to read data from store.

```js
const data = useSelector((state) => state.counter.count);
```

---

## useDispatch

Used to dispatch actions.

```js
dispatch(increment());
```

---

# 8. Folder Structure (Recommended)

```
src/
 ├── redux/
 │     ├── store.js
 │     ├── counterSlice.js
 ├── App.jsx
 ├── main.jsx
```

For larger apps:

```
redux/
 ├── store.js
 ├── features/
 │      ├── userSlice.js
 │      ├── cartSlice.js
 │      ├── productSlice.js
```

---

# 9. Async Actions (API Calls)

Redux Toolkit provides `createAsyncThunk`.

Example:

```js
import { createAsyncThunk } from "@reduxjs/toolkit";

export const fetchUsers = createAsyncThunk(
  "users/fetchUsers",
  async () => {
    const response = await fetch("https://jsonplaceholder.typicode.com/users");
    return response.json();
  }
);
```

Used inside slice with extraReducers.

---

# 10. Redux vs useState

| useState            | Redux                   |
| ------------------- | ----------------------- |
| Local state         | Global state            |
| Simple setup        | Structured architecture |
| Good for small apps | Best for large apps     |

---

# 11. When to Use Redux

Use Redux when:

* Large applications
* Complex state logic
* Many components share data
* Need predictable state management

Avoid Redux when:

* Small project
* Simple state logic

---

