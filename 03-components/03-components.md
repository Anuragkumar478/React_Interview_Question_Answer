# ⚛️ React Components – Interview Questions & Answers

> React component interview preparation — functional components, props, composition, lifecycle, component communication, and practical patterns.

---

## 1. What is a component in React?

A component is a **reusable piece of UI** that can contain its own:

* JSX
* Logic
* State
* Event handlers
* Props

Example:

```jsx
function Welcome() {
  return <h1>Welcome to React</h1>;
}
```

`Welcome` is a React component.

---

## 2. Why are components used in React?

Components help us divide a large application into smaller, reusable pieces.

For example, an e-commerce application might have:

```text
App
│
├── Navbar
├── SearchBar
├── CategoryFilter
├── ProductList
│   └── ProductCard
├── Cart
└── Footer
```

Benefits:

* Reusability
* Maintainability
* Easier testing
* Separation of responsibilities
* Easier debugging
* Better code organization

---

## 3. What are the types of components in React?

Historically, React had:

1. Functional Components
2. Class Components

Modern React primarily uses **functional components with Hooks**.

---

## 4. What is a functional component?

A functional component is a JavaScript function that returns React UI.

```jsx
function User() {
  return <h1>Anurag</h1>;
}
```

It can accept props:

```jsx
function User({ name }) {
  return <h1>{name}</h1>;
}
```

And it can use Hooks:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return <p>{count}</p>;
}
```

---

## 5. What is a class component?

A class component is a JavaScript class that extends `React.Component`.

```jsx
class User extends React.Component {
  render() {
    return <h1>{this.props.name}</h1>;
  }
}
```

Class components were widely used before Hooks.

Modern React applications generally prefer functional components.

---

## 6. Functional vs Class Components

| Functional Component      | Class Component        |
| ------------------------- | ---------------------- |
| JavaScript function       | JavaScript class       |
| Uses Hooks                | Uses lifecycle methods |
| Simpler syntax            | More verbose           |
| Preferred in modern React | Mostly legacy code     |
| Uses function body        | Uses `render()`        |

Example:

### Functional

```jsx
function User() {
  return <h1>User</h1>;
}
```

### Class

```jsx
class User extends React.Component {
  render() {
    return <h1>User</h1>;
  }
}
```

---

## 7. How do you create a component?

Create a JavaScript function that returns JSX.

```jsx
function Header() {
  return (
    <header>
      <h1>My Website</h1>
    </header>
  );
}

export default Header;
```

Then use it:

```jsx
import Header from "./Header";

function App() {
  return (
    <div>
      <Header />
    </div>
  );
}
```

---

## 8. What is a component tree?

A component tree represents the hierarchical relationship between components.

Example:

```text
App
│
├── Navbar
│   ├── Logo
│   └── Menu
│
├── Main
│   ├── ProductList
│   │   ├── ProductCard
│   │   ├── ProductCard
│   │   └── ProductCard
│   │
│   └── Sidebar
│
└── Footer
```

This structure makes it easier to understand how data and UI flow through an application.

---

## 9. What is component composition?

Composition means building complex UI by combining smaller components.

Example:

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

Usage:

```jsx
<Card>
  <h2>Product</h2>
  <p>₹500</p>
</Card>
```

Instead of creating one huge component, we compose smaller components together.

---

## 10. Why is composition preferred over inheritance in React?

React generally encourages **composition instead of inheritance** for code reuse.

For example:

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}
```

Different content can be inserted into the same component.

Composition provides flexibility without creating complicated inheritance hierarchies.

---

## 11. What are props in a component?

Props are inputs passed from a parent component to a child component.

```jsx
function App() {
  return <User name="Anurag" age={21} />;
}
```

Child:

```jsx
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

## 12. Are props mutable?

No.

Props should be treated as **read-only** by the receiving component.

Incorrect:

```jsx
function User(props) {
  props.name = "Rahul";
}
```

If a child needs a value to change, the parent can manage the state and pass down a callback.

---

## 13. Can a component receive multiple props?

Yes.

```jsx
<User
  name="Anurag"
  age={21}
  role="Developer"
  isActive={true}
/>
```

Child:

```jsx
function User({
  name,
  age,
  role,
  isActive
}) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
      <p>{role}</p>
      <p>{isActive ? "Active" : "Inactive"}</p>
    </div>
  );
}
```

---

## 14. What is props destructuring?

Instead of:

```jsx
function User(props) {
  return <h1>{props.name}</h1>;
}
```

we can destructure:

```jsx
function User({ name }) {
  return <h1>{name}</h1>;
}
```

This is cleaner and commonly used in React applications.

---

## 15. What is the `children` prop?

`children` contains whatever is placed between a component's opening and closing tags.

Example:

```jsx
function Card({ children }) {
  return (
    <div className="card">
      {children}
    </div>
  );
}
```

Usage:

```jsx
<Card>
  <h2>Hello</h2>
  <p>Welcome</p>
</Card>
```

The `<h2>` and `<p>` are received through `children`.

---

## 16. What is prop drilling?

Prop drilling occurs when data needs to be passed through multiple intermediate components even though those components don't directly need the data.

Example:

```text
App
 ↓ user
Dashboard
 ↓ user
Layout
 ↓ user
Profile
```

```jsx
<App user={user} />
```

Then:

```jsx
<Dashboard user={user} />
```

Then:

```jsx
<Layout user={user} />
```

Then:

```jsx
<Profile user={user} />
```

This can make code harder to maintain.

Possible solutions include:

* Context
* State management libraries
* Better component composition
* External stores

---

## 17. How can we avoid prop drilling?

For values needed by many components, React Context can be useful.

Example:

```jsx
const UserContext = createContext();

function App() {
  const user = {
    name: "Anurag"
  };

  return (
    <UserContext.Provider value={user}>
      <Dashboard />
    </UserContext.Provider>
  );
}
```

Then a nested component can consume the context.

```jsx
function Profile() {
  const user = useContext(UserContext);

  return <h1>{user.name}</h1>;
}
```

For complex application state, tools such as Redux Toolkit or external stores can also be appropriate.

---

## 18. What is component communication?

Components can communicate in different ways.

### Parent → Child

Using props.

```text
Parent
  ↓ props
Child
```

### Child → Parent

Using a callback passed from the parent.

```text
Parent
  ↑ callback
Child
```

### Sibling → Sibling

Usually by moving shared state to their common parent.

```text
     Parent
     /    \
 Child A  Child B
```

The parent manages the shared state and passes required data/callbacks to the children.

---

## 19. How does a child communicate with a parent?

The parent passes a function as a prop.

```jsx
function Parent() {
  const handleMessage = (message) => {
    console.log(message);
  };

  return <Child onMessage={handleMessage} />;
}
```

Child:

```jsx
function Child({ onMessage }) {
  return (
    <button onClick={() => onMessage("Hello Parent")}>
      Send
    </button>
  );
}
```

The child calls the parent's callback.

---

## 20. How do sibling components communicate?

Sibling components normally communicate through their common parent.

Example:

```text
          Parent
         /      \
   SearchBar   ProductList
```

The parent can store the search query:

```jsx
function Parent() {
  const [query, setQuery] = useState("");

  return (
    <>
      <SearchBar
        query={query}
        setQuery={setQuery}
      />

      <ProductList query={query} />
    </>
  );
}
```

This pattern is called **lifting state up**.

---

## 21. What is lifting state up?

Lifting state up means moving shared state to the closest common parent of components that need it.

Example:

```text
Before:

SearchBar → query
ProductList → needs query


After:

          Parent
         /      \
 SearchBar    ProductList
      ↑           ↑
      └── query ──┘
```

The parent becomes the source of truth.

---

## 22. What is a controlled component?

A controlled component is a component whose important input value is controlled by React state.

Example:

```jsx
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

React state controls the input value.

---

## 23. What is an uncontrolled component?

An uncontrolled component keeps its current input value in the DOM rather than React state.

A ref can be used to access the value.

```jsx
function Form() {
  const inputRef = useRef();

  const handleSubmit = () => {
    console.log(inputRef.current.value);
  };

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>
        Submit
      </button>
    </>
  );
}
```

---

## 24. Controlled vs Uncontrolled Components

| Controlled                   | Uncontrolled                   |
| ---------------------------- | ------------------------------ |
| Value managed by React state | Value managed by DOM           |
| Uses `value`                 | Often uses `defaultValue`      |
| Uses `onChange`              | Can use `ref`                  |
| Easier validation/control    | Can be simpler for basic forms |
| More explicit                | More DOM-driven                |

---

## 25. What is a pure component?

Conceptually, a pure component produces the same output when given the same inputs.

In modern React, `React.memo` can be used to skip re-rendering a component when its props have not changed according to its comparison.

Example:

```jsx
const User = React.memo(function User({ name }) {
  return <h1>{name}</h1>;
});
```

However, `React.memo` is a performance optimization, not something every component needs.

---

## 26. What is `React.memo()`?

`React.memo()` is a performance optimization that can prevent a function component from rendering again when its props are unchanged.

Example:

```jsx
const User = React.memo(function User({ name }) {
  return <h1>{name}</h1>;
});
```

If the parent renders again but `name` remains the same, React can reuse the previous result for that component.

### Important

`React.memo()` does not guarantee that a component will never render again.

---

## 27. What is the difference between `React.memo()` and `useMemo()`?

### `React.memo()`

Memoizes a **component's rendered result based on props**.

```jsx
const User = React.memo(UserComponent);
```

### `useMemo()`

Memoizes a **calculated value**.

```jsx
const filteredProducts = useMemo(
  () => products.filter(product => product.price > 500),
  [products]
);
```

---

## 28. What is the difference between `React.memo()` and `useCallback()`?

### `React.memo()`

Used to memoize a component.

```jsx
const Child = React.memo(ChildComponent);
```

### `useCallback()`

Used to memoize a function reference.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

They are often used together when a memoized child receives a callback prop.

---

## 29. What is a higher-order component (HOC)?

A Higher-Order Component is a function that takes a component and returns another component.

Conceptually:

```jsx
const EnhancedComponent = withAuth(Component);
```

Example:

```jsx
function withAuth(Component) {
  return function ProtectedComponent(props) {
    const isLoggedIn = true;

    if (!isLoggedIn) {
      return <Login />;
    }

    return <Component {...props} />;
  };
}
```

HOCs were historically common for reusing component logic.

Today, Hooks and composition are often preferred for many use cases.

---

## 30. What is component composition?

Composition means passing components or elements into another component.

Example:

```jsx
function Layout({ header, content, footer }) {
  return (
    <>
      {header}
      {content}
      {footer}
    </>
  );
}
```

Usage:

```jsx
<Layout
  header={<Navbar />}
  content={<Dashboard />}
  footer={<Footer />}
/>
```

This makes components flexible and reusable.

---

## 31. What is a presentational component?

A presentational component mainly focuses on displaying UI.

Example:

```jsx
function UserCard({ user }) {
  return (
    <div>
      <h2>{user.name}</h2>
      <p>{user.email}</p>
    </div>
  );
}
```

It generally contains little application/business logic.

---

## 32. What is a container component?

A container component traditionally handles data, state, or application logic and passes data to presentational components.

Example:

```jsx
function UserContainer() {
  const [user, setUser] = useState(null);

  // Fetch and manage user data

  return <UserCard user={user} />;
}
```

This distinction is a useful design concept, although modern React does not require strict container/presentational component separation.

---

## 33. What is a reusable component?

A reusable component is designed to work in multiple places with different inputs.

Example:

```jsx
function Button({ children, onClick, disabled }) {
  return (
    <button
      onClick={onClick}
      disabled={disabled}
    >
      {children}
    </button>
  );
}
```

Usage:

```jsx
<Button onClick={handleLogin}>
  Login
</Button>

<Button onClick={handleRegister}>
  Register
</Button>
```

---

## 34. What makes a good reusable component?

A good reusable component should generally have:

* Clear responsibility
* Flexible props
* Minimal unnecessary dependencies
* Predictable behavior
* Good naming
* Reasonable defaults
* Accessible UI
* Easy testing

Avoid creating components that are so generic that their API becomes difficult to understand.

---

## 35. What is component state?

Component state is data managed by a component that can change over time.

Example:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

When `count` changes, React schedules an update.

---

## 36. Can a component have multiple states?

Yes.

```jsx
function Form() {
  const [name, setName] = useState("");
  const [email, setEmail] = useState("");
  const [loading, setLoading] = useState(false);

  return (
    <form>
      {/* form */}
    </form>
  );
}
```

A component can have multiple independent state variables.

---

## 37. Can a component contain another component?

Yes.

```jsx
function App() {
  return (
    <div>
      <Navbar />
      <Dashboard />
    </div>
  );
}
```

`App` uses `Navbar` and `Dashboard` as child components.

---

## 38. Should components be defined inside other components?

Usually, reusable components should be defined outside their parent component.

Avoid:

```jsx
function App() {
  function User() {
    return <h1>User</h1>;
  }

  return <User />;
}
```

Prefer:

```jsx
function User() {
  return <h1>User</h1>;
}

function App() {
  return <User />;
}
```

Defining a component inside another component can create a new component definition during rendering and may lead to unnecessary remounting or lost state.

---

## 39. What is conditional component rendering?

A component can be rendered conditionally.

```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? (
        <Dashboard />
      ) : (
        <Login />
      )}
    </div>
  );
}
```

This is very common in authentication flows.

---

## 40. What is lazy loading a component?

Lazy loading allows a component's code to be loaded only when needed.

React provides:

```jsx
lazy()
```

Example:

```jsx
import { lazy, Suspense } from "react";

const Dashboard = lazy(
  () => import("./Dashboard")
);

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <Dashboard />
    </Suspense>
  );
}
```

This can reduce the initial JavaScript bundle.

---

## 41. What is `Suspense`?

`Suspense` allows React to display fallback UI while a child is waiting for something that supports Suspense.

A common use is lazy-loaded components.

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

The fallback is displayed while the lazy component is loading.

---

## 42. What is an error boundary?

An error boundary is a React component that catches rendering errors in its child component tree and displays fallback UI.

Traditional error boundaries are implemented using class component APIs such as:

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
      return <h1>Something went wrong.</h1>;
    }

    return this.props.children;
  }
}
```

Error boundaries do not catch every type of error, such as errors from ordinary event handlers.

---

## 43. What is component lifecycle?

A component goes through different stages.

Conceptually:

```text
Mount
  ↓
Update
  ↓
Unmount
```

### Mount

Component is added to the UI.

### Update

State or props change and React renders the component again.

### Unmount

Component is removed from the UI.

In functional components, Hooks such as `useEffect` can be used to synchronize with external systems during these stages.

---

## 44. What happens during mounting?

When a component is mounted:

1. React creates the component's UI representation.
2. React commits the necessary DOM changes.
3. Effects scheduled with `useEffect` run after the commit.

Example:

```jsx
useEffect(() => {
  console.log("Mounted");
}, []);
```

---

## 45. What happens when a component unmounts?

When a component is removed, React runs cleanup functions returned from its effects.

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

The cleanup prevents the timer from continuing after the component is unmounted.

---

## 46. What is a controlled component in a real MERN project?

Suppose your NGO application has a complaint form:

```jsx
function ComplaintForm() {
  const [title, setTitle] = useState("");
  const [description, setDescription] = useState("");

  return (
    <form>
      <input
        value={title}
        onChange={(e) => setTitle(e.target.value)}
      />

      <textarea
        value={description}
        onChange={(e) =>
          setDescription(e.target.value)
        }
      />
    </form>
  );
}
```

React controls the form values.

When submitted, the component can send the data to an Express API.

---

## 47. How would you structure components in an e-commerce React application?

A possible structure:

```text
src/
│
├── components/
│   ├── Navbar.jsx
│   ├── SearchBar.jsx
│   ├── ProductCard.jsx
│   ├── ProductList.jsx
│   └── Footer.jsx
│
├── pages/
│   ├── Home.jsx
│   ├── ProductDetails.jsx
│   ├── Cart.jsx
│   └── Login.jsx
│
├── hooks/
├── services/
├── context/
└── App.jsx
```

This keeps UI components, pages, reusable hooks, and API-related code organized.

---

## 48. How would you structure components in a MERN dashboard?

For example:

```text
Dashboard
│
├── Sidebar
├── Navbar
│
├── Statistics
│   ├── TotalUsers
│   ├── TotalComplaints
│   └── TotalDonations
│
├── Charts
│
└── RecentActivity
```

Each component should have a clear responsibility.

---

## 49. What is the difference between a component and a page?

A **component** is usually a reusable UI building block.

A **page** is typically a larger UI associated with a route.

Example:

```text
Pages
├── Home
├── Login
├── ProductDetails
└── Profile

Components
├── Navbar
├── Button
├── ProductCard
└── Modal
```

A page can contain many reusable components.

---

## 50. What is a component library?

A component library is a collection of reusable UI components.

Examples include:

* Buttons
* Modals
* Inputs
* Tables
* Cards
* Dropdowns
* Navigation components

Instead of recreating them for every page, developers can reuse standardized components.

---

# 🔥 Advanced Component Interview Questions

## 51. What is component re-rendering?

A component re-renders when React needs to evaluate it again because of an update such as:

* Its state changing
* Its parent rendering
* A consumed context value changing
* An external store update

A re-render does not necessarily mean the browser DOM is completely replaced.

---

## 52. Does a parent re-render cause the child to re-render?

A child may render again when its parent renders.

For example:

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        {count}
      </button>

      <Child />
    </>
  );
}
```

`Child` can render again when `Parent` renders.

If necessary, `React.memo()` can sometimes reduce such renders when the child's props have not changed.

---

## 53. Does `React.memo()` prevent all child re-renders?

No.

`React.memo()` only memoizes the component based on its props.

A memoized component can still render when:

* Its own state changes
* A context it consumes changes
* An external store it subscribes to changes
* Its props change

---

## 54. What is a component's responsibility?

A good component should ideally have a **clear and focused responsibility**.

For example:

```text
ProductCard
    ↓
Display product information

Cart
    ↓
Display/manage cart UI

SearchBar
    ↓
Handle search input
```

Avoid putting the entire application's logic inside one component.

---

## 55. What is component coupling?

Coupling describes how strongly components depend on each other.

High coupling:

```text
Component A
   ↓
Component B
   ↓
Component C
   ↓
Component D
```

Changes in one component may require changes in many others.

Good component design tries to keep unnecessary dependencies low.

---

## 56. What is component cohesion?

Cohesion describes how closely related the responsibilities inside a component are.

A component with high cohesion focuses on one related responsibility.

For example:

```jsx
function ProductPrice({ price }) {
  return <p>₹{price}</p>;
}
```

Its responsibility is clear.

---

## 57. What is the difference between composition and prop drilling?

### Composition

Pass UI/components into another component.

```jsx
<Card>
  <ProductInfo />
</Card>
```

### Prop drilling

Pass data through intermediate components that don't actually need it.

```text
App
 ↓
A
 ↓
B
 ↓
C
 ↓
D
```

Composition can sometimes reduce the need to pass data through unrelated intermediate components.

---

# 🎯 Most Important Component Questions

Before an interview, make sure you can answer these without looking at notes:

```text
1. What is a component?
2. Functional vs class component?
3. Why use components?
4. What is component composition?
5. What is props?
6. What is children?
7. What is prop drilling?
8. How do you avoid prop drilling?
9. What is lifting state up?
10. How does child communicate with parent?
11. How do sibling components communicate?
12. Controlled vs uncontrolled components?
13. What is React.memo?
14. React.memo vs useMemo?
15. React.memo vs useCallback?
16. What is an HOC?
17. What is lazy loading?
18. What is Suspense?
19. What is an error boundary?
20. What is component lifecycle?
21. What causes re-rendering?
22. Does parent re-render cause child re-render?
23. How should components be structured?
24. Composition vs inheritance?
25. How would you design components for a MERN project?
```

---

# 💼 MERN Interview Scenario

### Interviewer:

> You have a product page. The product data is fetched from an Express.js API. How would you divide the React UI into components?

### Good Answer:

I would divide the UI based on responsibility:

```text
ProductPage
│
├── Navbar
├── ProductDetails
│   ├── ProductImage
│   ├── ProductInfo
│   ├── ProductPrice
│   └── AddToCartButton
│
├── Reviews
│   └── ReviewCard
│
└── Footer
```

The page component can handle page-level data fetching or coordinate with a data-fetching layer, while smaller components focus mainly on displaying and interacting with specific parts of the UI.

For example:

```jsx
function ProductPage({ product }) {
  return (
    <>
      <Navbar />

      <ProductDetails product={product} />

      <Reviews productId={product._id} />

      <Footer />
    </>
  );
}
```

This approach makes the application easier to maintain, test, and extend.

---

# 🧠 One-Line Revision

```text
Component
   ↓
Reusable UI + Logic
   ↓
Props → Data from Parent
   ↓
State → Component's Dynamic Data
   ↓
Children → Nested Content
   ↓
Composition → Build Large UI from Small Components
   ↓
Lifting State → Share State Through Common Parent
   ↓
Context / Store → Avoid Excessive Prop Drilling
```

---

## ⭐ Interview Tip

Don't just memorize:

> "A component is a reusable piece of UI."

For a strong interview answer, explain:

> **What it is → why we use it → how it works → give a small example → connect it to a real project.**

For a MERN developer, be ready to explain how you would divide a real application such as an **e-commerce platform, NGO platform, or complaint-management system** into reusable React components.
