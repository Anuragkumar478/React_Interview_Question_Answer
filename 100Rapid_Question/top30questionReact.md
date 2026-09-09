# ⚛️ Top 30 React Interview Questions & Answers

A collection of the **30 most important React interview questions with simple, interview-ready answers**, especially useful for **Frontend and MERN Stack interviews**.

---

# 📌 React Basics

## 1. What is React?

**React** is a JavaScript library used to build user interfaces, especially single-page applications.

React was developed by **Meta (Facebook)**.

### Main features

* Component-based architecture
* Virtual DOM
* Declarative UI
* Reusable components
* State management
* Hooks

Example:

```jsx
function App() {
    return <h1>Hello React</h1>;
}

export default App;
```

---

## 2. What are the main features of React?

Important React features include:

* **Components** — Build UI using reusable components.
* **JSX** — Write HTML-like syntax inside JavaScript.
* **Virtual DOM** — Helps React efficiently update the UI.
* **Props** — Pass data from parent to child.
* **State** — Store data that can change.
* **Hooks** — Use state and lifecycle-related features in function components.
* **One-way data flow** — Data generally flows from parent to child.

---

## 3. What is JSX?

**JSX (JavaScript XML)** allows us to write HTML-like syntax inside JavaScript.

Example:

```jsx
const element = <h1>Hello World</h1>;
```

JSX is transformed into JavaScript during the build process.

For example:

```jsx
<h1>Hello</h1>
```

is conceptually transformed into a React element creation call.

### Interview Answer

> JSX makes writing React UI easier by allowing HTML-like syntax inside JavaScript.

---

## 4. What is a React component?

A component is a **reusable piece of UI**.

Example:

```jsx
function Welcome() {
    return <h1>Welcome to React</h1>;
}
```

We can use it:

```jsx
function App() {
    return (
        <div>
            <Welcome />
            <Welcome />
        </div>
    );
}
```

---

## 5. What is the difference between functional and class components?

### Functional Component

A JavaScript function that returns JSX.

```jsx
function User() {
    return <h1>Anurag</h1>;
}
```

### Class Component

A class extending `React.Component`.

```jsx
class User extends React.Component {
    render() {
        return <h1>Anurag</h1>;
    }
}
```

### Which is preferred?

Modern React primarily uses **function components and Hooks**.

---

## 6. What are Props in React?

**Props (properties)** are used to pass data from a parent component to a child component.

Parent:

```jsx
function App() {
    return <User name="Anurag" />;
}
```

Child:

```jsx
function User(props) {
    return <h1>Hello {props.name}</h1>;
}
```

Output:

```text
Hello Anurag
```

### Important

Props are **read-only** from the receiving component's perspective.

---

## 7. What is State in React?

State is data managed by a component that can change over time.

Example:

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <button onClick={() => setCount(count + 1)}>
            {count}
        </button>
    );
}
```

When state changes, React can re-render the component.

---

## 8. Difference between Props and State?

| Props                | State                               |
| -------------------- | ----------------------------------- |
| Passed from parent   | Managed by component                |
| Read-only            | Updated using state setter          |
| Used to pass data    | Used for changing data              |
| Controlled by parent | Usually controlled by the component |

Example:

```jsx
<User name="Anurag" />
```

`name` is a prop.

```jsx
const [count, setCount] = useState(0);
```

`count` is state.

### Interview Answer

> Props are used to pass data between components, while state is used to manage data that changes within a component.

---

# 🪝 React Hooks

## 9. What are Hooks?

Hooks are functions that allow function components to use React features such as state and effects.

Common Hooks:

```text
useState
useEffect
useContext
useRef
useMemo
useCallback
useReducer
```

Example:

```jsx
const [count, setCount] = useState(0);
```

---

## 10. What is `useState()`?

`useState()` is a Hook used to create and manage state in a function component.

```jsx
import { useState } from "react";

function Counter() {
    const [count, setCount] = useState(0);

    return (
        <div>
            <p>{count}</p>

            <button onClick={() => setCount(count + 1)}>
                Increase
            </button>
        </div>
    );
}
```

Here:

```text
count      → current state
setCount   → function used to update state
0          → initial value
```

---

## 11. What is `useEffect()`?

`useEffect()` is used to synchronize a component with external systems, such as:

* API requests
* Event listeners
* Timers
* Subscriptions
* Browser APIs

Example:

```jsx
import { useEffect } from "react";

useEffect(() => {
    console.log("Component rendered");
}, []);
```

The empty dependency array means the effect runs after the initial mount.

---

## 12. What is the dependency array in `useEffect()`?

Example:

```jsx
useEffect(() => {
    console.log("Effect");
}, [count]);
```

The effect runs after the initial mount and when `count` changes.

### Empty array

```jsx
useEffect(() => {
    console.log("Effect");
}, []);
```

Runs after the initial mount.

### No dependency array

```jsx
useEffect(() => {
    console.log("Effect");
});
```

Runs after every completed render where the effect is scheduled.

---

## 13. How do you clean up a `useEffect()`?

An effect can return a cleanup function.

Example:

```jsx
useEffect(() => {
    const timer = setInterval(() => {
        console.log("Running");
    }, 1000);

    return () => {
        clearInterval(timer);
    };
}, []);
```

Cleanup is useful for:

* Timers
* Event listeners
* Subscriptions
* Other resources created by the effect

---

## 14. What is `useRef()`?

`useRef()` creates a mutable ref object whose `.current` value persists between renders.

A common use is accessing a DOM element.

```jsx
import { useRef } from "react";

function App() {
    const inputRef = useRef(null);

    function focusInput() {
        inputRef.current.focus();
    }

    return (
        <>
            <input ref={inputRef} />
            <button onClick={focusInput}>
                Focus
            </button>
        </>
    );
}
```

Changing `ref.current` does **not** itself trigger a re-render.

---

## 15. What is `useMemo()`?

`useMemo()` memoizes the result of a calculation.

Example:

```jsx
const result = useMemo(() => {
    return expensiveCalculation(data);
}, [data]);
```

React can reuse the previously calculated value until a dependency changes.

### Important

Don't use `useMemo()` everywhere. It should be used when memoization provides a real performance benefit.

---

## 16. What is `useCallback()`?

`useCallback()` memoizes a function reference.

Example:

```jsx
const handleClick = useCallback(() => {
    console.log("Clicked");
}, []);
```

It can be useful when passing callbacks to memoized child components or when a stable function reference matters.

### Difference

```text
useMemo()
→ memoizes a calculated value

useCallback()
→ memoizes a function
```

---

# 🔄 React Rendering

## 17. What is the Virtual DOM?

The Virtual DOM is React's in-memory representation of the UI.

When state or props change, React:

```text
State/Props change
       ↓
React renders
       ↓
New UI representation
       ↓
React compares it with previous result
       ↓
Necessary DOM updates
```

This helps React update the browser efficiently.

### Important

> Virtual DOM is not simply a copy of the entire browser DOM that React manually replaces every time.

---

## 18. What is Reconciliation?

**Reconciliation** is the process React uses to determine what needs to change when the rendered UI changes.

React compares the previous rendered result with the new rendered result and commits the necessary updates.

Example:

Before:

```jsx
<h1>Hello</h1>
```

After:

```jsx
<h1>Hello Anurag</h1>
```

React can update the changed text rather than rebuilding unrelated DOM nodes.

---

## 19. What are Keys in React?

Keys help React identify items in a list.

Example:

```jsx
const users = [
    { id: 1, name: "Anurag" },
    { id: 2, name: "Rahul" }
];

function Users() {
    return (
        <ul>
            {users.map(user => (
                <li key={user.id}>
                    {user.name}
                </li>
            ))}
        </ul>
    );
}
```

### Why are keys important?

They help React correctly track list items when items are:

* Added
* Removed
* Reordered
* Updated

### Important

Prefer a **stable unique ID** rather than using the array index when the list can change.

---

## 20. What causes a React component to re-render?

Common causes include:

* Its state changes
* Its parent re-renders
* Its props change
* A consumed context value changes
* A subscribed external store changes

A re-render does **not necessarily mean the DOM is completely recreated**.

React determines which actual DOM changes are needed.

---

# 📦 Data & Component Communication

## 21. What is prop drilling?

Prop drilling means passing data through multiple intermediate components that don't actually need the data themselves.

Example:

```text
App
 ↓
Parent
 ↓
Child
 ↓
GrandChild
```

If `App` has data needed only by `GrandChild`, we may have to pass it through `Parent` and `Child`.

### Solutions

Depending on the situation:

* Context API
* State management libraries
* Component composition
* Better component structure

---

## 22. What is Context API?

Context allows data to be made available to components without manually passing props through every intermediate component.

Example:

```jsx
import { createContext } from "react";

const UserContext = createContext(null);
```

Provider:

```jsx
<UserContext.Provider value={user}>
    <Dashboard />
</UserContext.Provider>
```

Consumer:

```jsx
const user = useContext(UserContext);
```

Common use cases:

* Theme
* Current user
* Locale
* Application-level settings

---

## 23. What is lifting state up?

Lifting state up means moving shared state to the closest common parent of the components that need it.

Example:

```text
       Parent
      /      \
   Child A  Child B
```

If both children need the same state, keep the state in `Parent` and pass the required data/callbacks down.

### Interview Answer

> We lift state up when multiple components need to share the same state.

---

## 24. What is controlled vs uncontrolled component?

### Controlled

The input value is controlled by React state.

```jsx
function Form() {
    const [name, setName] = useState("");

    return (
        <input
            value={name}
            onChange={e => setName(e.target.value)}
        />
    );
}
```

React state is the source of truth.

### Uncontrolled

The DOM keeps the input value, often accessed with a ref.

```jsx
function Form() {
    const inputRef = useRef();

    return (
        <input ref={inputRef} />
    );
}
```

### Interview Answer

> Controlled inputs are managed through React state, while uncontrolled inputs keep their value in the DOM.

---

# 🧭 React Router & Performance

## 25. What is React Router?

React Router is a routing library commonly used to manage navigation between views in React applications.

Example:

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
    return (
        <BrowserRouter>
            <Routes>
                <Route
                    path="/"
                    element={<Home />}
                />

                <Route
                    path="/about"
                    element={<About />}
                />
            </Routes>
        </BrowserRouter>
    );
}
```

---

## 26. What is lazy loading in React?

Lazy loading means loading a component only when it is needed instead of loading everything initially.

Example:

```jsx
import { lazy, Suspense } from "react";

const About = lazy(() => import("./About"));

function App() {
    return (
        <Suspense fallback={<p>Loading...</p>}>
            <About />
        </Suspense>
    );
}
```

This can reduce the initial JavaScript bundle size.

---

## 27. What is `React.memo()`?

`React.memo()` is a performance optimization that can skip re-rendering a function component when its props have not changed according to React's memoization comparison.

Example:

```jsx
const User = React.memo(function User({ name }) {
    return <h1>{name}</h1>;
});
```

### Important

`React.memo()` is not necessary for every component.

Use it when avoiding a re-render provides a meaningful performance benefit.

---

# 🔥 Advanced React Questions

## 28. What is a custom Hook?

A custom Hook is a reusable JavaScript function whose name starts with `use` and that can use other Hooks.

Example:

```jsx
import { useState } from "react";

function useCounter(initialValue = 0) {
    const [count, setCount] = useState(initialValue);

    const increment = () => {
        setCount(c => c + 1);
    };

    return {
        count,
        increment
    };
}
```

Use it:

```jsx
function App() {
    const { count, increment } = useCounter(0);

    return (
        <>
            <p>{count}</p>
            <button onClick={increment}>
                Increase
            </button>
        </>
    );
}
```

### Benefit

Custom Hooks allow us to reuse **stateful logic** between components.

---

## 29. What are the Rules of Hooks?

There are two major rules:

### Rule 1

Only call Hooks at the **top level**.

Don't call them inside:

* Loops
* Conditions
* Nested functions

Wrong:

```jsx
if (isLoggedIn) {
    const [user, setUser] = useState(null);
}
```

Correct:

```jsx
const [user, setUser] = useState(null);

if (isLoggedIn) {
    // use user here
}
```

### Rule 2

Only call Hooks from:

* React function components
* Custom Hooks

---

## 30. How do you optimize a React application?

Common techniques include:

### 1. Avoid unnecessary re-renders

Use good component structure and, where justified:

```jsx
React.memo()
```

### 2. Memoize expensive calculations

```jsx
useMemo()
```

### 3. Memoize callbacks when useful

```jsx
useCallback()
```

### 4. Lazy load components

```jsx
lazy()
```

### 5. Use pagination or virtualization for large lists

Instead of rendering thousands of elements at once.

### 6. Optimize images

Use appropriate:

* Image dimensions
* Compression
* Modern formats
* Lazy loading where appropriate

### 7. Avoid unnecessary state

Keep state as close as practical to the components that need it.

### 8. Analyze before optimizing

Use React DevTools Profiler and browser performance tools to identify actual bottlenecks.

---

# ⭐ Most Important React Questions for MERN Interviews

If you have limited preparation time, prioritize these:

```text
1. What is React?
2. What is JSX?
3. Components
4. Props
5. State
6. Props vs State
7. useState
8. useEffect
9. useEffect dependency array
10. useRef
11. Virtual DOM
12. Reconciliation
13. Keys
14. Re-rendering
15. Prop drilling
16. Context API
17. Lifting state up
18. Controlled vs uncontrolled components
19. useMemo
20. useCallback
21. React.memo
22. Custom Hooks
23. Rules of Hooks
24. React Router
25. Lazy loading
26. Performance optimization
```

---

# 🎯 How to Answer React Questions in an Interview

For most React questions, use this structure:

```text
1. Definition
2. Why we use it
3. Small example
4. Important difference/pitfall
```

### Example

**Interviewer:** What is `useEffect`?

**Good answer:**

> `useEffect` is a React Hook used to synchronize a component with external systems such as API requests, timers, event listeners, or subscriptions. It runs after a render when its dependencies require it, and it can return a cleanup function. For example, I can use it to fetch data when a component mounts.

This is much stronger than simply saying:

> "`useEffect` is used for API calls."

---

# 🚀 Recommended MERN Interview Order

After HTML + CSS, prepare React in this order:

```text
HTML + CSS
     ↓
JavaScript
     ↓
React Basics
     ↓
React Hooks
     ↓
React Router
     ↓
API Integration
     ↓
State Management
     ↓
Node.js
     ↓
Express.js
     ↓
MongoDB
     ↓
Authentication / JWT
     ↓
Git & GitHub
     ↓
DSA
```

**Tip:** For React interviews, don't memorize only definitions. Practice explaining **your own projects** using these concepts—for example, where you used `useState`, `useEffect`, Context, routing, API calls, authentication, and reusable components.
