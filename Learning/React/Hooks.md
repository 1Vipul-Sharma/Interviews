# React Hooks Interview Questions & Answers

This guide covers React Hooks interview questions with **definitions, industry usage, and examples** — designed to help you stand out in interviews.

---

## 1. What are React Hooks?

**Definition:**  
Hooks are functions introduced in React 16.8 that let developers use state and other React features (like lifecycle methods) in functional components without writing class components.

**Industry Usage:**

- Simplifies code by avoiding class components.
- Encourages reusable logic through **custom hooks**.
- Widely used in production apps for state management, data fetching, and side effects.

**Example:**

```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);
  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}
```

---

## 2. What is `useState`?

**Definition:**  
`useState` is a Hook that lets you add and manage state in functional components.

**Industry Usage:**

- Track UI states (dark/light theme).
- Manage form inputs.
- Store local component data in dashboards, e-commerce carts, etc.

**Example:**

```jsx
const [theme, setTheme] = useState("light");
```

---

## 3. What is `useEffect`?

**Definition:**  
`useEffect` is used for performing side effects in functional components (e.g., data fetching, subscriptions, logging).

**Industry Usage:**

- Fetching data from APIs in dashboards or e-commerce apps.
- Listening to WebSocket/real-time updates.
- Syncing data to localStorage.

**Example:**

```jsx
useEffect(() => {
  fetch("/api/products")
    .then((res) => res.json())
    .then((data) => setProducts(data));
}, []);
```

---

## 4. What is `useContext`?

**Definition:**  
`useContext` provides a way to access values from React’s Context API directly, avoiding prop drilling.

**Industry Usage:**

- Managing authentication states (JWT token, user roles).
- Theme toggling across an application.
- Sharing global settings (language, permissions).

**Example:**

```jsx
const AuthContext = React.createContext();

function App() {
  return (
    <AuthContext.Provider value={{ user: "Vipul" }}>
      <Profile />
    </AuthContext.Provider>
  );
}

function Profile() {
  const { user } = useContext(AuthContext);
  return <h1>Welcome {user}</h1>;
}
```

---

## 5. What is `useReducer`?

**Definition:**  
`useReducer` is a Hook used for state management, especially when the state logic is complex or involves multiple sub-values.

**Industry Usage:**

- Handling large forms with multiple input states.
- Managing cart logic in e-commerce apps.
- Alternative to Redux in smaller apps.

**Example:**

```jsx
const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
};

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

---

## 6. What is `useMemo`?

**Definition:**  
`useMemo` memoizes a computed value, recalculating only when dependencies change.

**Industry Usage:**

- Optimizing performance in large lists.
- Preventing expensive calculations from re-running unnecessarily.

**Example:**

```jsx
const sortedProducts = useMemo(() => {
  return products.sort((a, b) => a.price - b.price);
}, [products]);
```

---

## 7. What is `useCallback`?

**Definition:**  
`useCallback` memoizes a function, ensuring the same instance is used between renders unless dependencies change.

**Industry Usage:**

- Passing stable callbacks to child components to prevent unnecessary re-renders.
- Used heavily with `React.memo` for optimization.

**Example:**

```jsx
const handleAddToCart = useCallback(() => {
  console.log("Added to cart");
}, []);
```

---

## 8. What are Custom Hooks?

**Definition:**  
Custom Hooks are user-defined functions that reuse logic by leveraging existing Hooks.

**Industry Usage:**

- Abstract API calls into reusable hooks (`useFetch`).
- Manage authentication (`useAuth`).
- Real-time subscriptions (`useChat`, `useSocket`).

**Example:**

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then(setData);
  }, [url]);

  return data;
}
```

---

## 9. Difference between `useEffect` and `useLayoutEffect`?

- `useEffect` → runs asynchronously after paint (non-blocking).
- `useLayoutEffect` → runs synchronously before the browser paints (blocking).

**Industry Usage:**

- `useEffect` → API calls, subscriptions.
- `useLayoutEffect` → DOM measurement, animations.

---

## 10. Common mistakes with Hooks?

1. Using Hooks inside loops/conditions (must be top-level).
2. Forgetting dependency arrays in `useEffect`.
3. Not memoizing callbacks leading to unnecessary re-renders.
4. Confusing `useMemo` and `useCallback`.

---

# Final Tip

In industry, Hooks are used for:

- **State management (useState, useReducer).**
- **Side effects & async calls (useEffect).**
- **Performance optimization (useMemo, useCallback).**
- **Context & global state (useContext, custom hooks).**

Mastering these will show strong **React ecosystem knowledge** in interviews.
