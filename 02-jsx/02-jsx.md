# ⚛️ React Basics – Interview Questions & Answers

> React.js interview preparation — from beginner to intermediate level.

---

## 1. What is React?

React is a **JavaScript library** developed by Meta for building user interfaces, especially interactive web applications.

React follows a **component-based architecture**, where the UI is divided into reusable components.

### Key Features

* Component-based architecture
* JSX
* Declarative UI
* Virtual DOM and reconciliation
* One-way data flow
* Hooks
* Reusable components
* Large ecosystem

### Example

```jsx
function App() {
  return <h1>Hello React</h1>;
}

export default App;
```

---

## 2. Why do we use React?

React makes it easier to build complex and interactive user interfaces.

### Advantages

1. **Reusable Components**
2. **Efficient UI Updates**
3. **Declarative Programming**
4. **Large Ecosystem**
5. **Easy Integration with APIs**
6. **Strong Community Support**
7. **Easy to build scalable applications**

---

## 3. Is React a library or a framework?

React is a **JavaScript library**.

React mainly focuses on the **UI layer**.

For example, React itself does not force you to use a particular solution for:

* Routing
* State management
* API calls
* Form management

You can choose libraries such as:

* React Router
* Redux Toolkit
* TanStack Query
* Axios

### Interview Answer

> React is a JavaScript library for building user interfaces. Unlike a complete framework, React mainly focuses on the UI layer and allows developers to choose additional libraries for routing, state management, and other requirements.

---

## 4. What are the main features of React?

Important React features include:

### 1. Components

UI is divided into reusable components.

### 2. JSX

Allows us to write HTML-like syntax inside JavaScript.

### 3. Virtual DOM

React maintains an internal representation of the UI and reconciles changes efficiently.

### 4. One-Way Data Flow

Data generally flows from parent components to child components through props.

### 5. Hooks

Hooks allow function components to use state and other React features.

Examples:

```jsx
useState()
useEffect()
useContext()
useRef()
useMemo()
useCallback()
```

---

## 5. What is a component in React?

A component is a **reusable piece of UI**.

A component usually contains:

* UI
* Logic
* State
* Event handling

### Example

```jsx
function Welcome() {
  return <h1>Welcome to React</h1>;
}
```

Here, `Welcome` is a React component.

---

## 6. What are the types of components in React?

Historically, React had two major types:

### 1. Functional Components

```jsx
function User() {
  return <h1>Anurag</h1>;
}
```

### 2. Class Components

```jsx
class User extends React.Component {
  render() {
    return <h1>Anurag</h1>;
  }
}
```

Modern React primarily uses **functional components with Hooks**.

---

## 7. What is a functional component?

A functional component is a JavaScript function that returns React elements.

```jsx
function App() {
  return (
    <div>
      <h1>Hello</h1>
    </div>
  );
}
```

It can use Hooks such as:

```jsx
useState()
useEffect()
useContext()
```

---

## 8. What is a class component?

A class component is a JavaScript class that extends `React.Component`.

```jsx
class App extends React.Component {
  render() {
    return <h1>Hello React</h1>;
  }
}
```

Class components were widely used before Hooks were introduced.

Today, functional components are generally preferred for new React code.

---

## 9. What is JSX?

JSX stands for **JavaScript XML**.

It allows us to write HTML-like syntax inside JavaScript.

```jsx
const element = <h1>Hello World</h1>;
```

JSX is transformed by the React toolchain into JavaScript that React can use to create elements.

---

## 10. Is JSX mandatory in React?

No.

JSX is **not mandatory**.

You can create React elements using JavaScript APIs as well.

For example:

```jsx
const element = React.createElement(
  "h1",
  null,
  "Hello World"
);
```

However, JSX makes UI code much easier to read and maintain.

---

## 11. What are the advantages of JSX?

### Advantages

* Easier to read
* Easier to write UI
* Supports JavaScript expressions
* Helps structure components
* Makes component code more maintainable

Example:

```jsx
function User({ name }) {
  return <h1>Hello {name}</h1>;
}
```

---

## 12. Can we write JavaScript inside JSX?

Yes.

JavaScript expressions can be written inside `{}`.

```jsx
function App() {
  const name = "Anurag";

  return <h1>Hello {name}</h1>;
}
```

Another example:

```jsx
const age = 21;

return <p>{age >= 18 ? "Adult" : "Minor"}</p>;
```

---

## 13. What is a React element?

A React element is an object describing what should appear in the UI.

Example:

```jsx
const element = <h1>Hello</h1>;
```

A component returns React elements.

### Important

**Component ≠ Element**

A component is a reusable function/class, while an element is a description of UI.

---

## 14. What is the difference between React and JavaScript?

| JavaScript                           | React                              |
| ------------------------------------ | ---------------------------------- |
| Programming language                 | JavaScript library                 |
| Used for general-purpose programming | Mainly used for building UI        |
| Can run without React                | Built using JavaScript             |
| Provides language features           | Provides UI/component abstractions |

Example:

```javascript
const name = "Anurag";
```

React:

```jsx
function App() {
  return <h1>{name}</h1>;
}
```

---

## 15. What is one-way data flow in React?

React generally follows **one-way data flow**.

Data flows:

```text
Parent
   ↓
Child
   ↓
Grandchild
```

For example:

```jsx
function Parent() {
  const name = "Anurag";

  return <Child name={name} />;
}

function Child({ name }) {
  return <h1>{name}</h1>;
}
```

The parent passes `name` to the child using props.

---

## 16. What are props?

Props are **read-only inputs** passed from a parent component to a child component.

Example:

```jsx
function App() {
  return <User name="Anurag" age={21} />;
}

function User({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
    </div>
  );
}
```

Here:

```text
name
age
```

are props.

---

## 17. Can a child component modify its props?

No.

Props should be treated as **read-only**.

Incorrect:

```jsx
function Child(props) {
  props.name = "Rahul";
}
```

If a child needs to request a change, the parent can provide a callback function.

```jsx
function Parent() {
  const handleChange = () => {
    console.log("Changed");
  };

  return <Child onChange={handleChange} />;
}
```

---

## 18. What is state in React?

State is data that belongs to a component and can change over time.

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

Here:

```text
count → current state
setCount → function to update state
```

---

## 19. What is the difference between props and state?

| Props                | State                           |
| -------------------- | ------------------------------- |
| Passed from parent   | Managed by component            |
| Read-only            | Can be updated                  |
| Used to pass data    | Used for dynamic data           |
| Controlled by parent | Usually controlled by component |

Example:

```jsx
<User name="Anurag" />
```

`name` is a prop.

```jsx
const [count, setCount] = useState(0);
```

`count` is state.

---

## 20. What happens when state changes?

When React state changes, React schedules an update.

React then:

1. Re-renders the relevant component
2. Creates the new UI representation
3. Compares it with the previous representation
4. Commits necessary changes to the DOM

Example:

```jsx
setCount(count + 1);
```

This causes React to update the UI where necessary.

---

## 21. What is the Virtual DOM?

The Virtual DOM is a common term for React's **in-memory representation of the UI**.

When state or props change, React creates a new representation, compares it with the previous one, and determines what needs to change in the actual DOM.

This process is called **reconciliation**.

---

## 22. What is reconciliation in React?

Reconciliation is the process React uses to determine how the UI should change after an update.

For example:

```text
Old UI
   ↓
State changes
   ↓
New UI representation
   ↓
React compares
   ↓
Required DOM updates
```

React avoids unnecessarily replacing the entire DOM tree.

---

## 23. What is the difference between DOM and Virtual DOM?

| DOM                                 | React's UI representation           |
| ----------------------------------- | ----------------------------------- |
| Browser's actual document structure | In-memory representation            |
| Directly affects the page           | Used by React during reconciliation |
| Browser-managed                     | React-managed representation        |

The important point is that React does not simply update the entire DOM after every state change.

---

## 24. What is declarative programming in React?

In declarative programming, we describe **what the UI should look like**, rather than manually describing every DOM operation.

Example:

```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? <Dashboard /> : <Login />}
    </div>
  );
}
```

We describe the desired UI.

React handles the update process.

---

## 25. What is imperative DOM manipulation?

Imperative code explicitly tells the browser what operations to perform.

Example:

```javascript
const element = document.getElementById("message");

element.textContent = "Hello";
element.style.color = "red";
```

React generally encourages declarative UI instead.

---

## 26. What is component-based architecture?

Component-based architecture divides an application into small reusable components.

Example:

```text
App
│
├── Navbar
├── Sidebar
├── ProductList
│   └── ProductCard
└── Footer
```

Each component can contain its own:

* UI
* Logic
* State
* Event handlers

This makes applications easier to maintain and scale.

---

## 27. Why are components useful?

Components provide:

### Reusability

```jsx
<ProductCard />
<ProductCard />
<ProductCard />
```

### Maintainability

Large applications can be divided into smaller pieces.

### Separation of concerns

Different UI responsibilities can be handled by different components.

### Testability

Smaller components are generally easier to test.

---

## 28. What is the entry point of a React application?

In a typical modern React application created with tools such as Vite, the entry point is commonly:

```text
src/main.jsx
```

Example:

```jsx
import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

`createRoot()` creates a React root and renders the application into the DOM element.

---

## 29. What is `createRoot()`?

`createRoot()` is used to create a React root for rendering an application.

Example:

```jsx
import { createRoot } from "react-dom/client";

const root = createRoot(
  document.getElementById("root")
);

root.render(<App />);
```

It is the modern API used by React 18+ applications.

---

## 30. What is StrictMode?

`StrictMode` is a development-only tool that helps identify potential problems in a React application.

Example:

```jsx
<StrictMode>
  <App />
</StrictMode>
```

It can intentionally perform additional development checks, including extra effect setup/cleanup behavior, to help identify bugs.

It does **not** add visible UI to the application.

---

## 31. What are keys in React?

Keys help React identify items in a list.

Example:

```jsx
const users = [
  { id: 1, name: "Anurag" },
  { id: 2, name: "Rahul" }
];

function Users() {
  return (
    <div>
      {users.map(user => (
        <p key={user.id}>
          {user.name}
        </p>
      ))}
    </div>
  );
}
```

The `key` should be stable and unique among siblings.

---

## 32. Why should we not use array index as a key?

Using the index as a key can cause problems when list items are:

* Reordered
* Inserted
* Removed

Example:

```jsx
users.map((user, index) => (
  <User key={index} user={user} />
));
```

A stable ID is usually better:

```jsx
users.map(user => (
  <User key={user.id} user={user} />
));
```

Index keys can be acceptable for truly static lists where the order never changes.

---

## 33. What is conditional rendering?

Conditional rendering means displaying UI based on a condition.

Example:

```jsx
function App({ isLoggedIn }) {
  if (isLoggedIn) {
    return <Dashboard />;
  }

  return <Login />;
}
```

Using a ternary:

```jsx
return isLoggedIn ? <Dashboard /> : <Login />;
```

Using `&&`:

```jsx
return isAdmin && <AdminPanel />;
```

---

## 34. What is rendering in React?

Rendering is the process where React evaluates a component and determines the UI representation it should produce.

Example:

```jsx
function App() {
  return <h1>Hello</h1>;
}
```

When state or props change, React may render the component again and then reconcile the result.

---

## 35. What causes a React component to re-render?

Common causes include:

### 1. State update

```jsx
setCount(count + 1);
```

### 2. Parent re-render

A child may render again when its parent renders.

### 3. Context value changes

Components consuming changed context may re-render.

### 4. External store updates

Components subscribed to an external store may re-render when the store changes.

---

## 36. Does re-render mean the DOM is completely updated?

No.

A component can re-render without React replacing the entire DOM.

React compares the new UI representation with the previous one and commits the necessary host-tree changes.

---

## 37. What is a Single Page Application (SPA)?

A Single Page Application loads the main application shell and updates the UI dynamically without requiring a full browser page reload for every navigation.

React is commonly used to build SPAs, often together with React Router.

Example:

```text
/products
/products/10
/cart
/profile
```

The application can switch views while remaining within the same browser document.

---

## 38. Is React only used for Single Page Applications?

No.

React can be used for:

* SPAs
* Server-rendered applications
* Static websites
* Dashboards
* E-commerce applications
* Mobile applications through React Native
* Full-stack applications through frameworks such as Next.js

---

## 39. What is React Native?

React Native is a framework for building native mobile applications using React and JavaScript/TypeScript.

It is different from React for the web.

```text
React
  ↓
Web UI

React Native
  ↓
Mobile UI
```

---

## 40. What is the difference between React and React Native?

| React            | React Native               |
| ---------------- | -------------------------- |
| Web applications | Mobile applications        |
| Uses DOM         | Uses native platform UI    |
| `<div>`          | `<View>`                   |
| `<button>`       | `<Pressable>` / `<Button>` |
| Runs in browser  | Runs on mobile platforms   |

---

# ⭐ Quick Interview Revision

Before an interview, remember these points:

```text
React
 ↓
JavaScript UI Library
 ↓
Component-Based
 ↓
JSX
 ↓
Props + State
 ↓
One-Way Data Flow
 ↓
Reconciliation
 ↓
Hooks
 ↓
Declarative UI
```

### Most Important Questions

1. What is React?
2. Why use React?
3. Library vs framework?
4. What is JSX?
5. What is a component?
6. Functional vs class component?
7. What are props?
8. What is state?
9. Props vs state?
10. What is reconciliation?
11. What is the Virtual DOM?
12. What causes re-rendering?
13. What are keys?
14. Why avoid index as key?
15. What is StrictMode?
16. What is `createRoot()`?
17. What is conditional rendering?
18. What is one-way data flow?
19. What is declarative programming?
20. React vs React Native?

---

# 🎯 Interview Tip

For every React question, try to answer in this order:

```text
Definition
    ↓
Why it is used
    ↓
How it works
    ↓
Small code example
    ↓
Real project example
```

For a MERN interview, connect your answers to real applications such as:

```text
React
 ↓
Components
 ↓
Props / State
 ↓
API calls
 ↓
Authentication
 ↓
MongoDB-backed Express API
```
