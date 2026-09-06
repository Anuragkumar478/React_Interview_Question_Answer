# ⚛️ Advanced React — Interview Questions & Answers

A practical collection of advanced React interview questions covering Context, custom Hooks, Suspense, Error Boundaries, portals, refs, concurrent rendering, SSR, hydration, Server Components, and advanced architecture.

---

# 📌 1. What are advanced concepts in React?

Important advanced React concepts include:

* Context API
* Custom Hooks
* Error Boundaries
* Portals
* Suspense
* Lazy loading
* Concurrent rendering
* `useTransition`
* `useDeferredValue`
* Refs and imperative APIs
* `forwardRef`
* Higher-Order Components
* Render props
* Compound components
* SSR
* Hydration
* Streaming
* Server Components
* Advanced state management

---

# 🧠 Context API

## 📌 2. What is Context API?

Context allows data to be shared with components without passing props manually through every intermediate component.

Example:

```jsx
const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Dashboard />
    </ThemeContext.Provider>
  );
}
```

Then:

```jsx
const theme = useContext(ThemeContext);
```

---

## 📌 3. What problem does Context solve?

It mainly helps solve **prop drilling**.

Without Context:

```text
App
 ↓ props
Dashboard
 ↓ props
Sidebar
 ↓ props
UserProfile
```

With Context:

```text
App
 ↓
Context
 ↓
UserProfile
```

The component can directly consume the required context.

---

## 📌 4. Is Context a replacement for Redux?

Not always.

Context is mainly a mechanism for providing values to a component subtree.

Redux is a dedicated state-management solution with features such as:

* Centralized state
* Actions
* Reducers
* Middleware
* DevTools
* Predictable state transitions

For simple shared values, Context may be enough.

For complex application state, a dedicated state-management solution may be more appropriate.

---

# 🧩 Custom Hooks

## 📌 5. What is a Custom Hook?

A custom Hook is a JavaScript function whose name starts with `use` and which can use other Hooks.

Example:

```jsx
function useOnlineStatus() {
  const [online, setOnline] = useState(navigator.onLine);

  useEffect(() => {
    const handleOnline = () => setOnline(true);
    const handleOffline = () => setOnline(false);

    window.addEventListener("online", handleOnline);
    window.addEventListener("offline", handleOffline);

    return () => {
      window.removeEventListener("online", handleOnline);
      window.removeEventListener("offline", handleOffline);
    };
  }, []);

  return online;
}
```

Use it:

```jsx
function App() {
  const online = useOnlineStatus();

  return <p>{online ? "Online" : "Offline"}</p>;
}
```

---

## 📌 6. Why are Custom Hooks useful?

They allow you to reuse **stateful logic**.

For example:

```text
useAuth()
useFetch()
useDebounce()
useOnlineStatus()
useLocalStorage()
usePagination()
```

Instead of duplicating the same logic across components.

---

## 📌 7. Do Custom Hooks share state?

No.

Each call to a Custom Hook gets its own Hook state.

```jsx
const user1 = useUser();
const user2 = useUser();
```

These are separate instances unless the Hook internally uses shared state such as Context or an external store.

---

# 🚨 Error Boundaries

## 📌 8. What is an Error Boundary?

An Error Boundary is a React component that catches certain rendering errors in its child component tree and displays fallback UI instead of allowing the entire affected UI tree to crash.

Conceptually:

```text
Application
     ↓
Error Boundary
     ↓
Dashboard
     ↓
Broken Component
```

The boundary can show:

```text
Something went wrong.
Please try again.
```

---

## 📌 9. What errors do Error Boundaries catch?

They can catch errors during:

* Rendering
* Lifecycle methods
* Constructors of descendant class components

They do not automatically catch every type of error, such as:

* Event-handler errors
* Server-side errors
* Errors in asynchronous callbacks
* Errors thrown by the boundary itself

---

## 📌 10. Can a function component itself be an Error Boundary?

React's traditional Error Boundary API is class-based.

Example:

```jsx
class ErrorBoundary extends React.Component {
  state = {
    hasError: false
  };

  static getDerivedStateFromError() {
    return {
      hasError: true
    };
  }

  componentDidCatch(error, info) {
    console.error(error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong.</h2>;
    }

    return this.props.children;
  }
}
```

---

# 🪟 Portals

## 📌 11. What is a React Portal?

A Portal allows React to render a component into a different DOM node while keeping it within the same React tree.

Example:

```jsx
createPortal(
  <Modal />,
  document.getElementById("modal-root")
);
```

---

## 📌 12. Where are Portals useful?

Common examples:

* Modals
* Dialogs
* Tooltips
* Dropdowns
* Toast notifications
* Overlay components

Example:

```text
React Root
│
├── App
│
└── Modal
       ↓
   #modal-root
```

---

## 📌 13. Do events work normally through Portals?

Yes.

Events from portal content participate in React's event system according to the React tree, even though the DOM node is mounted somewhere else.

This is one reason Portals are useful for overlays.

---

# 🎯 Refs

## 📌 14. What is useRef?

`useRef` stores a mutable value that persists across renders without causing a re-render when the value changes.

```jsx
const inputRef = useRef(null);
```

Then:

```jsx
<input ref={inputRef} />
```

You can access:

```jsx
inputRef.current.focus();
```

---

## 📌 15. When should you use refs?

Common use cases:

* Accessing DOM elements
* Focusing inputs
* Storing timer IDs
* Integrating third-party libraries
* Keeping mutable values that don't affect rendering

---

## 📌 16. useRef vs useState

| useState                   | useRef                                      |
| -------------------------- | ------------------------------------------- |
| Updates cause re-render    | Updating `.current` doesn't cause re-render |
| Used for UI state          | Used for mutable values/DOM references      |
| React tracks state updates | React doesn't render based on ref changes   |

---

# 🔗 forwardRef

## 📌 17. What is forwardRef?

Historically, `forwardRef` has been used to allow a parent to pass a ref through a component to a child DOM element or component.

Conceptually:

```jsx
const Input = forwardRef((props, ref) => {
  return <input ref={ref} {...props} />;
});
```

Parent:

```jsx
const inputRef = useRef();

<Input ref={inputRef} />
```

This is useful for reusable input components and imperative APIs.

> React's newer versions also provide improved ref handling, so always follow the API conventions of the React version used by your project.

---

# 🧠 Higher-Order Components

## 📌 18. What is a Higher-Order Component?

A Higher-Order Component (HOC) is a function that takes a component and returns an enhanced component.

```jsx
function withAuth(Component) {
  return function ProtectedComponent(props) {
    if (!isAuthenticated()) {
      return <Login />;
    }

    return <Component {...props} />;
  };
}
```

Usage:

```jsx
const ProtectedDashboard = withAuth(Dashboard);
```

---

## 📌 19. Is HOC commonly used in modern React?

Hooks and composition are often preferred for new code.

HOCs are still important because:

* Older React codebases use them
* Libraries may use similar patterns
* They are a common interview topic

---

# 🎨 Render Props

## 📌 20. What is the Render Props pattern?

A component uses a function prop to decide what UI should be rendered.

Example:

```jsx
<DataProvider
  render={(data) => <ProductList products={data} />}
/>
```

The component controls the logic while the caller controls the UI.

---

## 📌 21. Render Props vs Custom Hooks

### Render Props

```text
Logic + function passed as prop
```

### Custom Hook

```text
Logic extracted into reusable Hook
```

Modern React applications generally prefer Custom Hooks for many reusable-logic cases because they are often simpler to compose.

---

# 🧩 Compound Components

## 📌 22. What are Compound Components?

Compound components work together to form a flexible component API.

Example:

```jsx
<Tabs>
  <Tabs.List>
    <Tabs.Tab>Home</Tabs.Tab>
    <Tabs.Tab>Profile</Tabs.Tab>
  </Tabs.List>

  <Tabs.Panel>Home Content</Tabs.Panel>
  <Tabs.Panel>Profile Content</Tabs.Panel>
</Tabs>
```

Internally, they can share state through Context.

---

## 📌 23. Why use Compound Components?

They provide:

* Flexible APIs
* Better component composition
* Reusable UI patterns
* Separation of behavior and presentation

Common examples:

```text
Tabs
Accordion
Menu
Select
Modal
```

---

# 💤 Suspense

## 📌 24. What is Suspense?

`Suspense` allows React to display fallback UI while something in a supported part of the tree is not ready.

Example:

```jsx
<Suspense fallback={<Loading />}>
  <Dashboard />
</Suspense>
```

---

## 📌 25. What is Suspense commonly used for?

One common use is lazy-loaded components:

```jsx
const Dashboard = lazy(() => import("./Dashboard"));

<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

Suspense is also used by some frameworks and data-loading systems for supported asynchronous rendering patterns.

---

# 📦 Lazy Loading

## 📌 26. What is React.lazy?

It dynamically loads a component.

```jsx
const Admin = React.lazy(() => import("./Admin"));
```

Then:

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Admin />
</Suspense>
```

This enables code splitting.

---

# ⚡ Concurrent Rendering

## 📌 27. What is concurrent rendering?

Modern React can schedule rendering work so that urgent interactions can remain responsive while less urgent work is processed.

The key idea is:

> React can prioritize work rather than treating every update as equally urgent.

---

## 📌 28. What is startTransition?

`startTransition` marks an update as non-urgent.

```jsx
startTransition(() => {
  setSearchResults(results);
});
```

This can help React keep urgent UI interactions responsive.

---

## 📌 29. What is useTransition?

`useTransition` provides a way to start a transition and know whether the transition is pending.

```jsx
const [isPending, startTransition] = useTransition();
```

Example:

```jsx
startTransition(() => {
  setTab("dashboard");
});
```

---

## 📌 30. What is useDeferredValue?

It provides a deferred version of a value.

```jsx
const deferredQuery = useDeferredValue(query);
```

This is useful when a rapidly changing value drives expensive rendering.

---

## 📌 31. useTransition vs useDeferredValue

| useTransition                      | useDeferredValue                |
| ---------------------------------- | ------------------------------- |
| Marks a state update as non-urgent | Defers a value                  |
| You control the update             | You control the value           |
| Provides `isPending`               | No equivalent pending flag      |
| Useful for transitions             | Useful for expensive derived UI |

---

# 🌐 SSR

## 📌 32. What is Server-Side Rendering?

SSR means rendering HTML for a request on the server and sending HTML to the browser.

Conceptually:

```text
Browser
   ↓
Server
   ↓
React renders HTML
   ↓
HTML sent to browser
```

Frameworks such as Next.js provide SSR capabilities.

---

## 📌 33. SSR vs CSR

### CSR

```text
Browser
 ↓
JavaScript
 ↓
React renders UI
```

### SSR

```text
Browser
 ↓
Server
 ↓
HTML
 ↓
Browser
 ↓
JavaScript hydration
```

SSR can improve initial content delivery and can help with SEO, depending on the application.

---

# 💧 Hydration

## 📌 34. What is hydration?

Hydration is the process where React attaches its client-side behavior to HTML that was already rendered on the server.

Example:

```text
Server-rendered HTML
        ↓
      Browser
        ↓
   React JavaScript
        ↓
    Hydration
        ↓
Interactive application
```

---

## 📌 35. What is a hydration mismatch?

A hydration mismatch occurs when the server-rendered output doesn't match what React expects to render on the client.

Potential causes include:

```jsx
new Date()
Math.random()
window-dependent rendering
```

when their results differ between server and client.

---

# 🚀 Streaming

## 📌 36. What is streaming SSR?

Instead of waiting for the entire page to be generated, the server can stream HTML progressively to the browser.

Conceptually:

```text
Server
 ↓
Header
 ↓
Main content
 ↓
Additional content
 ↓
Page complete
```

This can improve perceived loading performance.

---

# 🧠 React Server Components

## 📌 37. What are React Server Components?

React Server Components allow certain components to run on the server rather than being included as client-side JavaScript.

This can reduce client-side JavaScript for suitable parts of an application.

They are commonly associated with frameworks such as Next.js.

---

## 📌 38. Server Component vs Client Component

Conceptually:

### Server Component

Runs on the server and is suitable for server-side data access and non-interactive UI.

### Client Component

Runs in the browser and is needed for interactive behavior such as:

```jsx
useState()
useEffect()
onClick
```

The exact conventions depend on the framework.

---

# 🔐 Security

## 📌 39. Does React automatically make an application secure?

No.

React provides some protections, such as escaping text inserted through normal JSX rendering.

But developers must still protect against:

* XSS
* CSRF
* Broken authentication
* Authorization issues
* Insecure API endpoints
* Sensitive data exposure

---

## 📌 40. Why should dangerouslySetInnerHTML be used carefully?

Example:

```jsx
<div
  dangerouslySetInnerHTML={{
    __html: html
  }}
/>
```

This bypasses React's normal text escaping behavior.

If `html` contains untrusted content, it can introduce XSS vulnerabilities.

Only use it with properly trusted or sanitized HTML.

---

# 🧠 Architecture

## 📌 41. What is component composition?

Composition means building complex UI by combining smaller components.

Example:

```jsx
<Card>
  <CardHeader />
  <CardBody />
  <CardFooter />
</Card>
```

Instead of creating one giant component.

---

## 📌 42. Why is composition preferred over excessive inheritance?

React encourages composition.

Instead of:

```text
BaseComponent
    ↓
ExtendedComponent
    ↓
AdvancedComponent
```

use:

```text
Page
 ├── Header
 ├── Card
 ├── Button
 └── Footer
```

This usually makes components easier to reuse and maintain.

---

# 🧠 Controlled vs Imperative APIs

## 📌 43. What is declarative programming in React?

You describe **what the UI should look like** based on state.

```jsx
return isLoggedIn
  ? <Dashboard />
  : <Login />;
```

You don't manually tell the browser:

```text
Find element
Change HTML
Add class
Remove element
```

React manages the DOM updates.

---

## 📌 44. What is imperative programming?

Imperative programming describes **how to perform an operation** step by step.

Example:

```jsx
inputRef.current.focus();
```

This directly asks the DOM element to perform an action.

React is primarily declarative, but refs provide controlled escape hatches for imperative behavior.

---

# 📌 Advanced Hooks

## 📌 45. What is useId?

`useId` generates stable IDs suitable for associating elements such as labels and inputs.

```jsx
const id = useId();

<label htmlFor={id}>Email</label>
<input id={id} />
```

It is particularly useful in reusable components and server-rendered applications.

---

## 📌 46. Why shouldn't useId be used for list keys?

Keys need to represent item identity.

For list items, use the item's stable data ID:

```jsx
items.map(item => (
  <Item key={item.id} />
));
```

`useId` is designed for IDs used in accessibility and DOM relationships, not list identity.

---

# 🧪 Strict Mode

## 📌 47. What is React Strict Mode?

Strict Mode is a development-time tool that helps identify potential problems.

```jsx
<StrictMode>
  <App />
</StrictMode>
```

It does not represent production behavior in exactly the same way.

In development, React may intentionally invoke certain logic more than once to expose unsafe side effects.

---

## 📌 48. Why does useEffect sometimes appear to run twice in development?

With Strict Mode in development, React may perform an additional setup/cleanup cycle to help detect effects that are not implemented correctly.

This does not mean you should simply remove Strict Mode.

Instead, make effects properly:

* Setup
* Cleanup
* Repeat safely

---

# 📌 External Stores

## 📌 49. What is useSyncExternalStore?

`useSyncExternalStore` is a React Hook designed for subscribing to external stores in a way that integrates correctly with React's rendering model.

It can be useful for:

* State libraries
* Browser APIs
* External subscriptions

Most application developers will use it indirectly through libraries rather than calling it frequently themselves.

---

# 🧠 Advanced Performance

## 📌 50. What is memoization?

Memoization means caching a previous result so that expensive work doesn't need to be repeated when inputs haven't changed.

React provides tools such as:

```text
React.memo
useMemo
useCallback
```

Use them selectively.

---

## 📌 51. What is referential equality?

Objects and functions are compared by reference.

```jsx
const a = {};
const b = {};

console.log(a === b); // false
```

Even though they contain the same data, they are different object references.

This matters for:

* `React.memo`
* `useMemo`
* `useCallback`
* Dependency arrays
* Context values
* Redux selectors

---

# 📌 Advanced Component Patterns

## 📌 52. What is a reusable component API?

A reusable component should provide a flexible interface without exposing unnecessary implementation details.

Example:

```jsx
<Button
  variant="primary"
  size="large"
  onClick={handleSubmit}
>
  Submit
</Button>
```

Good component APIs improve:

* Reusability
* Consistency
* Maintainability

---

## 📌 53. What is the principle of component composition?

Instead of making a component handle every possible use case, provide smaller composable pieces.

Example:

```jsx
<Modal>
  <Modal.Header />
  <Modal.Body />
  <Modal.Footer />
</Modal>
```

This gives consumers more control.

---

# 📌 React + MERN Architecture

## 📌 54. How would you design a scalable React frontend for a MERN application?

Example:

```text
src/
│
├── components/
├── pages/
├── layouts/
├── hooks/
├── services/
├── store/
├── context/
├── utils/
├── routes/
└── assets/
```

Example flow:

```text
React UI
   ↓
Custom Hooks
   ↓
API Service
   ↓
Express API
   ↓
MongoDB
```

Authentication:

```text
React
  ↓
Cookie/session or token-based auth
  ↓
Express middleware
  ↓
Authorization
  ↓
Controller
  ↓
MongoDB
```

---

# 📌 55. How would you handle authentication in React?

Typical architecture:

```text
Login Form
    ↓
POST /api/auth/login
    ↓
Backend validates credentials
    ↓
Authentication established
    ↓
Frontend fetches current user
    ↓
Protected UI
```

Frontend route protection is useful for navigation and UX, but **real authorization must be enforced by the backend**.

---

# 📌 56. How would you handle global authentication state?

Possible approaches:

### Context

```text
AuthProvider
   ↓
useAuth()
```

### Redux

```text
authSlice
   ↓
useSelector()
```

### External state library

For example, Zustand or another appropriate store.

Choose based on application complexity rather than automatically making everything global.

---

# 📌 57. How do you prevent unnecessary API requests?

Use techniques such as:

* Debouncing
* Caching
* Request cancellation
* Pagination
* Conditional fetching
* Avoiding duplicate effects
* Reusing fetched data
* Server-state libraries when appropriate

---

# 📌 58. How do you handle real-time data in React?

For a MERN application using Socket.IO:

```text
React
  ↓
Socket.IO
  ↓
Node.js
  ↓
Database
```

Example:

```jsx
useEffect(() => {
  socket.on("complaintUpdated", handleUpdate);

  return () => {
    socket.off("complaintUpdated", handleUpdate);
  };
}, []);
```

Always clean up subscriptions.

---

# 📌 59. What is an imperative handle?

`useImperativeHandle` allows a component to customize the value exposed through a ref.

Conceptually:

```jsx
useImperativeHandle(ref, () => ({
  focus() {
    inputRef.current.focus();
  }
}));
```

This can be useful when a reusable component needs to expose a small imperative API.

Use it sparingly because React's preferred style is declarative.

---

# 🎯 Advanced Interview Questions

## Q1. What is the difference between Context and Redux?

**Context** primarily provides values through a component tree.

**Redux** provides a structured state-management architecture with centralized state, actions, reducers, middleware, and tooling.

---

## Q2. What is a Custom Hook?

A reusable function that uses React Hooks to share stateful logic between components.

---

## Q3. What is an Error Boundary?

A mechanism for catching certain rendering errors in a descendant component tree and displaying fallback UI.

---

## Q4. What is a Portal?

A way to render React content into a different DOM location while keeping it connected to the same React tree.

---

## Q5. What is Suspense?

A React mechanism for displaying fallback UI while supported content is not yet ready.

---

## Q6. What is hydration?

The process of attaching React's client-side behavior to server-rendered HTML.

---

## Q7. What is concurrent rendering?

A React rendering capability that allows work to be scheduled and prioritized so urgent interactions can remain responsive.

---

## Q8. What is useTransition?

A Hook for marking state updates as non-urgent and tracking whether the transition is pending.

---

## Q9. What is useDeferredValue?

A Hook that provides a deferred version of a value so expensive rendering can lag behind urgent updates.

---

## Q10. What is React Server Components?

A React architecture where some components execute on the server and don't need to be sent to the browser as client-side JavaScript.

---

# 🚀 Advanced React Quick Revision

```text
Advanced React
│
├── Context
│   ├── Avoid prop drilling
│   └── Shared values
│
├── Custom Hooks
│   └── Reusable stateful logic
│
├── Error Boundary
│   └── Rendering error fallback
│
├── Portals
│   └── Modal / Tooltip / Overlay
│
├── Refs
│   ├── DOM access
│   └── Imperative APIs
│
├── Patterns
│   ├── HOC
│   ├── Render Props
│   └── Compound Components
│
├── Suspense
│   └── Loading boundaries
│
├── Performance
│   ├── memo
│   ├── useMemo
│   ├── useCallback
│   ├── useTransition
│   └── useDeferredValue
│
├── Server Rendering
│   ├── SSR
│   ├── Hydration
│   └── Streaming
│
└── Modern React
    └── Server Components
```

---

# ⭐ 1-Minute Advanced React Interview Answer

If the interviewer asks:

> **"What advanced React concepts do you know?"**

You can answer:

> "I have worked with advanced React concepts such as Context API, Custom Hooks, memoization using React.memo, useMemo and useCallback, refs, Portals, Suspense and lazy loading, error boundaries, and performance optimization. I also understand concurrent rendering concepts such as useTransition and useDeferredValue, along with SSR, hydration, streaming, and the role of React Server Components. For scalable applications, I focus on component composition, reusable hooks, proper state ownership, API abstraction, and keeping authorization on the backend."

---

# 🎯 Final React Interview Roadmap

```text
01 React Basics
       ↓
02 JSX
       ↓
03 Components
       ↓
04 Props & State
       ↓
05 Hooks
       ↓
06 Rendering & Virtual DOM
       ↓
07 Forms & Events
       ↓
08 State Management
       ↓
09 React Router
       ↓
10 API Integration
       ↓
11 Performance Optimization
       ↓
12 Advanced React
```

## 🔥 Most Important Topics to Master

For a **MERN Stack Developer interview**, prioritize:

```text
⭐⭐⭐⭐⭐ Hooks
⭐⭐⭐⭐⭐ Props & State
⭐⭐⭐⭐⭐ API Integration
⭐⭐⭐⭐⭐ React Router
⭐⭐⭐⭐⭐ State Management
⭐⭐⭐⭐⭐ Performance
⭐⭐⭐⭐  Context API
⭐⭐⭐⭐  Custom Hooks
⭐⭐⭐⭐  Error Boundaries
⭐⭐⭐⭐  Suspense / Lazy Loading
⭐⭐⭐    Portals
⭐⭐⭐    SSR / Hydration
⭐⭐⭐    Concurrent Rendering
⭐⭐     Server Components
```

> **Interview rule:** Don't just memorize definitions. Be able to explain **why the concept exists, when to use it, when not to use it, and how you used it in a real MERN project.**
