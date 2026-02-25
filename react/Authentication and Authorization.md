# Authentication and Authorization

## 1. What is Authentication?

Authentication verifies **who the user is**.

Example:

* Login with Email & Password
* Login with Google
* Login with OTP

Result:

* User identity is confirmed.

Example flow:

User → Login Form → Server → Verify Credentials → Token Generated

---

## 2. What is Authorization?

Authorization verifies **what the user is allowed to access**.

Examples:

* Admin can delete users
* Student can view courses only
* Trainer can upload content

Authentication happens first, then authorization.

---

## 3. Why Use Redux for Authentication?

Redux helps to:

* Store logged-in user globally
* Access user data in any component
* Protect routes
* Maintain login state after refresh

Central Store Example:

```
Redux Store
   |
   |-- auth
         |-- user
         |-- token
         |-- isAuthenticated
```

---

## 4. Install Required Packages

Create React project:

```
npx create-react-app auth-app
cd auth-app
```

Install Redux Toolkit:

```
npm install @reduxjs/toolkit react-redux react-router-dom
```

---

## 5. Project Structure

```
src/
│
├── app/
│     store.js
│
├── features/
│     auth/
│          authSlice.js
│
├── pages/
│     Login.js
│     Dashboard.js
│
├── components/
│     ProtectedRoute.js
│
└── App.js
```

---

## 6. Create Redux Store

### app/store.js

```js
import { configureStore } from "@reduxjs/toolkit";
import authReducer from "../features/auth/authSlice";

export const store = configureStore({
  reducer: {
    auth: authReducer,
  },
});
```

---

## 7. Provide Store to React

### index.js

```js
import React from "react";
import ReactDOM from "react-dom/client";
import { Provider } from "react-redux";
import { store } from "./app/store";
import App from "./App";

const root = ReactDOM.createRoot(document.getElementById("root"));

root.render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

---

## 8. Create Authentication Slice

### features/auth/authSlice.js

```js
import { createSlice } from "@reduxjs/toolkit";

const initialState = {
  user: null,
  token: null,
  isAuthenticated: false,
};

const authSlice = createSlice({
  name: "auth",
  initialState,
  reducers: {
    loginSuccess: (state, action) => {
      state.user = action.payload.user;
      state.token = action.payload.token;
      state.isAuthenticated = true;
    },

    logout: (state) => {
      state.user = null;
      state.token = null;
      state.isAuthenticated = false;
    },
  },
});

export const { loginSuccess, logout } = authSlice.actions;
export default authSlice.reducer;
```

---

## 9. Login Page

### pages/Login.js

```js
import { useDispatch } from "react-redux";
import { loginSuccess } from "../features/auth/authSlice";
import { useNavigate } from "react-router-dom";

export default function Login() {
  const dispatch = useDispatch();
  const navigate = useNavigate();

  const handleLogin = () => {
    const fakeUser = {
      user: { name: "Varun", role: "admin" },
      token: "123456",
    };

    dispatch(loginSuccess(fakeUser));
    navigate("/dashboard");
  };

  return (
    <div>
      <h2>Login Page</h2>
      <button onClick={handleLogin}>Login</button>
    </div>
  );
}
```

---

## 10. Dashboard Page

### pages/Dashboard.js

```js
import { useSelector, useDispatch } from "react-redux";
import { logout } from "../features/auth/authSlice";

export default function Dashboard() {
  const user = useSelector((state) => state.auth.user);
  const dispatch = useDispatch();

  return (
    <div>
      <h2>Dashboard</h2>
      <h3>Welcome {user?.name}</h3>
      <button onClick={() => dispatch(logout())}>
        Logout
      </button>
    </div>
  );
}
```

---

## 11. Protected Route (Authorization)

### components/ProtectedRoute.js

```js
import { useSelector } from "react-redux";
import { Navigate } from "react-router-dom";

export default function ProtectedRoute({ children }) {
  const isAuth = useSelector(
    (state) => state.auth.isAuthenticated
  );

  if (!isAuth) {
    return <Navigate to="/" />;
  }

  return children;
}
```

---

## 12. Setup Routing

### App.js

```js
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Login from "./pages/Login";
import Dashboard from "./pages/Dashboard";
import ProtectedRoute from "./components/ProtectedRoute";

function App() {
  return (
    <BrowserRouter>
      <Routes>

        <Route path="/" element={<Login />} />

        <Route
          path="/dashboard"
          element={
            <ProtectedRoute>
              <Dashboard />
            </ProtectedRoute>
          }
        />

      </Routes>
    </BrowserRouter>
  );
}

export default App;
```

---

## 13. Role-Based Authorization

Example:

```js
if (user.role !== "admin") {
  return <h1>Access Denied</h1>;
}
```

Roles:

* admin
* trainer
* student

---

## 14. Token Storage (Optional)

Save token:

```js
localStorage.setItem("token", token);
```

Load on refresh:

```js
const token = localStorage.getItem("token");
```

---

## 15. Authentication Flow

1. User submits login form
2. API verifies credentials
3. Token received
4. Token stored in Redux
5. Protected routes enabled
6. Logout clears state

---

