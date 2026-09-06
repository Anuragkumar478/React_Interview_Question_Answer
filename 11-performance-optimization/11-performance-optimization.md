# ⚡ React Performance Optimization — Interview Questions & Answers

A complete guide to React performance optimization, from basic concepts to advanced interview questions.

---

## 📌 1. What is performance optimization in React?

Performance optimization means improving an application's:

* Rendering speed
* Responsiveness
* Memory usage
* Network performance
* Initial load time
* User interaction speed

The goal is to avoid unnecessary work while keeping the application maintainable.

---

## 📌 2. What causes performance problems in React?

Common causes include:

* Unnecessary re-renders
* Large lists
* Expensive calculations
* Large JavaScript bundles
* Unoptimized images
* Too many API requests
* Missing pagination
* Poor state management
* Unnecessary Context updates
* Excessive component complexity

---

## 📌 3. What is a re-render?

A re-render means React calls a component again to calculate what its UI should look like.

```jsx
function App() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

When `count` changes, `App` re-renders.

**Important:**

> Re-render does not automatically mean the real DOM is updated.

React compares the new result with the previous result and commits only necessary DOM changes.

---

## 📌 4. What is the difference between re-render and DOM update?

### Re-render

React executes the component again.

### DOM update

React actually changes something in the browser DOM.

Example:

```jsx
function App() {
  const [count, setCount] = useState(0);

  return (
    <>
      <h1>Hello</h1>
      <p>{count}</p>
    </>
  );
}
```

When `count` changes, the component re-renders, but React doesn't need to recreate the entire DOM.

---

# 🧠 React.memo

## 📌 5. What is React.memo?

`React.memo` prevents a component from re-rendering when its props have not changed.

```jsx
const User = React.memo(function User({ name }) {
  return <h2>{name}</h2>;
});
```

If the parent re-renders but `name` remains the same, React can skip rendering `User`.

---

## 📌 6. How does React.memo compare props?

By default, `React.memo` performs a shallow comparison of props.

Primitive values:

```jsx
<User name="Anurag" />
```

are easy to compare.

But objects and arrays use reference equality:

```jsx
<User user={{ name: "Anurag" }} />
```

A new object is created on every render, so the prop reference changes.

---

## 📌 7. When should you use React.memo?

Use it when:

* A component renders frequently
* Rendering is relatively expensive
* Parent components re-render often
* Props usually remain unchanged

Don't blindly wrap every component with `React.memo`.

---

## 📌 8. Is React.memo always beneficial?

No.

`React.memo` itself has a comparison cost.

For a very cheap component, the comparison may provide little or no benefit.

Therefore:

> Optimize based on actual performance problems rather than memoizing everything.

---

# 🧠 useMemo

## 📌 9. What is useMemo?

`useMemo` caches the result of an expensive calculation.

```jsx
const filteredProducts = useMemo(() => {
  return products.filter(product =>
    product.name.toLowerCase().includes(search.toLowerCase())
  );
}, [products, search]);
```

React recalculates the value only when dependencies change.

---

## 📌 10. Why is useMemo useful?

Suppose:

```jsx
const result = expensiveCalculation(data);
```

If the component re-renders many times, this calculation runs repeatedly.

With:

```jsx
const result = useMemo(() => {
  return expensiveCalculation(data);
}, [data]);
```

React can reuse the previous result when `data` has not changed.

---

## 📌 11. Should useMemo be used everywhere?

No.

Avoid:

```jsx
const name = useMemo(() => "Anurag", []);
```

This provides no meaningful benefit.

Use `useMemo` when:

* Calculation is expensive
* Recalculation happens frequently
* Dependencies often remain unchanged

---

# 🧠 useCallback

## 📌 12. What is useCallback?

`useCallback` caches a function reference.

```jsx
const handleDelete = useCallback((id) => {
  deleteProduct(id);
}, []);
```

This can be useful when passing callbacks to memoized child components.

---

## 📌 13. Why can functions cause unnecessary re-renders?

Consider:

```jsx
function Parent() {
  const handleClick = () => {
    console.log("Clicked");
  };

  return <Child onClick={handleClick} />;
}
```

Every time `Parent` renders, a new function reference is created.

Therefore:

```jsx
handleClick !== previousHandleClick
```

A memoized child may then re-render because its prop changed by reference.

---

## 📌 14. How does useCallback help?

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

React can preserve the function reference between renders until dependencies change.

It is especially useful with:

```jsx
React.memo(Child)
```

---

## 📌 15. useMemo vs useCallback

| Hook          | Caches               |
| ------------- | -------------------- |
| `useMemo`     | A computed value     |
| `useCallback` | A function reference |

Example:

```jsx
const total = useMemo(() => calculateTotal(cart), [cart]);

const handleCheckout = useCallback(() => {
  checkout(cart);
}, [cart]);
```

---

# 📌 Component Rendering

## 📌 16. Does a parent re-render cause children to re-render?

Normally, when a parent component re-renders, its child components may also render.

Example:

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

`Child` can re-render when `Parent` renders.

Using:

```jsx
const Child = React.memo(...)
```

can allow React to skip the child when its props are unchanged.

---

## 📌 17. How can you reduce unnecessary re-renders?

Common techniques:

1. Keep state close to where it is used
2. Use `React.memo` where useful
3. Use `useMemo` for expensive calculations
4. Use `useCallback` when stable callback references matter
5. Split large components
6. Avoid unnecessary Context updates
7. Use virtualization for large lists
8. Avoid unnecessary state

---

# 📌 State Optimization

## 📌 18. What is state colocation?

State colocation means keeping state as close as possible to the components that use it.

Bad:

```text
App
 └── Global State
      ├── Header
      ├── Product
      ├── Footer
      └── Search
```

Better:

```text
App
 ├── Header
 ├── Product
 └── Search
      └── Search State
```

Don't move every piece of state into global state.

---

## 📌 19. Why can unnecessary state hurt performance?

Every state update can trigger a render of the component that owns that state and potentially affect descendants.

For example, don't store:

```jsx
const [fullName, setFullName] = useState("");
```

if it can simply be derived from:

```jsx
const fullName = `${firstName} ${lastName}`;
```

Avoid redundant state when the value can be calculated reliably.

---

# 📌 Lists

## 📌 20. Why are keys important for performance?

Keys help React identify list items across renders.

```jsx
products.map(product => (
  <Product
    key={product._id}
    product={product}
  />
));
```

Stable keys help React preserve component identity and efficiently reconcile lists.

---

## 📌 21. Why should array indexes usually not be used as keys?

Avoid:

```jsx
products.map((product, index) => (
  <Product key={index} product={product} />
));
```

If items are inserted, deleted, or reordered, indexes can refer to different items.

Prefer a stable unique ID:

```jsx
<Product key={product._id} />
```

---

# 📌 Large Lists

## 📌 22. What is list virtualization?

Virtualization means rendering only the items currently visible in the viewport instead of rendering thousands of items simultaneously.

For example:

```text
10,000 products
       ↓
Only ~20 visible products rendered
```

This can significantly reduce DOM work.

Libraries such as `react-window` can be used for this technique.

---

## 📌 23. When should you use virtualization?

Use it when:

* Lists are very large
* Many DOM nodes cause performance problems
* Users only see a small portion of the list at a time

For a list of 20 products, virtualization is usually unnecessary.

---

# 📌 Pagination

## 📌 24. How does pagination improve performance?

Instead of requesting:

```text
100,000 products
```

request:

```text
20 products
```

Example:

```http
GET /api/products?page=1&limit=20
```

Benefits:

* Smaller API response
* Less memory usage
* Faster rendering
* Less database/network work

---

## 📌 25. Pagination vs infinite scrolling

### Pagination

```text
Page 1 → Page 2 → Page 3
```

Good for:

* Admin dashboards
* Search results
* Tables

### Infinite scrolling

```text
Load more
↓
Load more
↓
Load more
```

Good for:

* Social feeds
* Product feeds
* Content discovery

---

# 📌 Lazy Loading

## 📌 26. What is lazy loading?

Lazy loading means loading something only when it is needed.

Instead of loading every page/component immediately:

```text
Application
 ├── Home
 ├── Dashboard
 ├── Admin
 └── Reports
```

you can load less frequently used sections later.

---

## 📌 27. What is React.lazy?

`React.lazy` allows a component to be loaded dynamically.

```jsx
const Dashboard = React.lazy(() => import("./Dashboard"));
```

Then:

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Dashboard />
</Suspense>
```

---

## 📌 28. What is code splitting?

Code splitting divides the JavaScript bundle into smaller chunks.

Instead of:

```text
main.js = 2 MB
```

you may have:

```text
main.js
dashboard.js
admin.js
profile.js
```

Only required chunks need to be loaded initially.

---

## 📌 29. How does route-based code splitting work?

Example:

```jsx
const Dashboard = lazy(() => import("./pages/Dashboard"));
const Admin = lazy(() => import("./pages/Admin"));
```

The dashboard code can be loaded when the user navigates to `/dashboard`.

This reduces initial JavaScript work.

---

# 📌 Bundle Optimization

## 📌 30. What is bundle size?

Bundle size is the amount of JavaScript/CSS/etc. that must be downloaded and processed by the browser.

Large bundles can increase:

* Initial load time
* JavaScript parsing
* Execution time
* Memory usage

---

## 📌 31. How can you reduce bundle size?

Techniques include:

* Code splitting
* Lazy loading
* Removing unused dependencies
* Tree shaking
* Using production builds
* Avoiding unnecessarily large libraries
* Optimizing imports

---

## 📌 32. What is tree shaking?

Tree shaking removes unused code from the production bundle when the build tooling can determine that it is unused.

Modern bundlers such as Vite support production optimizations including tree shaking.

---

# 📌 Image Optimization

## 📌 33. How do images affect React performance?

Large images can significantly increase page load time.

Example:

```text
5 MB image
      ↓
Slow network
      ↓
Slow page loading
```

Use:

* WebP/AVIF where appropriate
* Proper dimensions
* Compression
* Responsive images
* Lazy loading for below-the-fold images

---

## 📌 34. How can images be lazy-loaded?

For normal images:

```jsx
<img
  src="/product.webp"
  loading="lazy"
  alt="Product"
/>
```

Don't blindly lazy-load the main above-the-fold/LCP image because delaying it can hurt loading performance.

---

# 📌 Web Performance

## 📌 35. What are Core Web Vitals?

Important user-experience metrics include:

### LCP — Largest Contentful Paint

Measures loading performance of the main visible content.

### INP — Interaction to Next Paint

Measures responsiveness to user interactions.

### CLS — Cumulative Layout Shift

Measures unexpected layout movement.

---

## 📌 36. How can you improve LCP?

Possible techniques:

* Optimize the main image
* Reduce server response time
* Reduce render-blocking resources
* Use caching
* Reduce unnecessary JavaScript
* Use CDN delivery where appropriate

---

## 📌 37. How can you improve INP?

Reduce long-running JavaScript work.

Techniques:

* Split expensive work
* Avoid unnecessary renders
* Optimize event handlers
* Use transitions for non-urgent UI updates
* Break up expensive tasks

---

## 📌 38. How can you improve CLS?

Avoid unexpected layout changes.

For example, reserve image space:

```css
img {
  aspect-ratio: 16 / 9;
}
```

or provide explicit dimensions.

---

# 📌 API Performance

## 📌 39. How can API calls affect React performance?

Too many API requests can cause:

* Slow UI
* Network congestion
* Increased server load
* Duplicate requests
* Poor user experience

Example:

```text
Search:
r
re
rea
reac
react
```

could create five API requests.

---

## 📌 40. What is debouncing?

Debouncing waits until the user stops performing an action before executing the function.

Example:

```text
Typing:
r → re → rea → reac → react

API call:
             ↓
          "react"
```

Useful for search boxes.

---

## 📌 41. What is throttling?

Throttling limits how frequently a function can execute.

Example:

```text
Scroll events:
|||||||||||||||||||||

Function:
|---|---|---|---|
```

Useful for:

* Scroll events
* Mouse movement
* Resize events

---

## 📌 42. Debouncing vs throttling

| Debouncing                 | Throttling                 |
| -------------------------- | -------------------------- |
| Waits for activity to stop | Limits execution frequency |
| Search input               | Scroll                     |
| Form validation            | Mouse movement             |
| Autocomplete               | Resize                     |

---

# 📌 Request Cancellation

## 📌 43. Why should API requests sometimes be cancelled?

Suppose a user searches:

```text
react
```

and then quickly searches:

```text
redux
```

The earlier request may finish later and incorrectly overwrite the newer result.

Cancellation can prevent unnecessary work and stale responses.

Using `fetch`:

```jsx
const controller = new AbortController();

fetch("/api/products", {
  signal: controller.signal
});

return () => controller.abort();
```

---

# 📌 Context Performance

## 📌 44. Can Context API cause performance problems?

Yes.

When a Context value changes, consumers that read that context may re-render.

For example:

```jsx
<AuthContext.Provider value={{ user, login }}>
```

If the provider value is recreated frequently, consumers can receive a new context value.

---

## 📌 45. How can Context performance be improved?

Possible techniques:

* Split contexts
* Keep providers appropriately scoped
* Avoid putting unrelated state into one context
* Memoize provider values when useful
* Keep frequently changing state local when possible

Example:

```text
AuthContext
CartContext
ThemeContext
```

instead of one huge:

```text
AppContext
```

---

# 📌 React Profiler

## 📌 46. What is React Profiler?

React DevTools Profiler helps identify rendering performance problems.

It can help answer:

* Which component rendered?
* How often did it render?
* How long did rendering take?
* What caused the render?

---

## 📌 47. How should you optimize a slow React component?

Don't guess.

Follow this process:

```text
Identify problem
      ↓
Measure
      ↓
Find expensive component/work
      ↓
Optimize
      ↓
Measure again
```

This is better than adding `useMemo` and `useCallback` everywhere.

---

# 📌 useTransition

## 📌 48. What is useTransition?

`useTransition` lets React mark an update as non-urgent.

```jsx
const [isPending, startTransition] = useTransition();

startTransition(() => {
  setSearchQuery(value);
});
```

This can help keep urgent interactions responsive while React works on less urgent updates.

---

## 📌 49. What is useDeferredValue?

`useDeferredValue` lets you use a deferred version of a value.

```jsx
const deferredQuery = useDeferredValue(query);
```

This can be useful when rendering based on a rapidly changing value is expensive.

For example:

```text
User typing
    ↓
Input remains responsive
    ↓
Expensive results update can lag slightly
```

---

# 📌 Forms Performance

## 📌 50. How can large forms cause performance problems?

If every keystroke updates large amounts of React state, many components may re-render.

For large forms:

* Split components
* Keep state close to where it is used
* Avoid unnecessary parent re-renders
* Consider specialized form libraries when appropriate
* Validate efficiently

---

# 📌 Redux Performance

## 📌 51. How can Redux cause unnecessary re-renders?

Components using:

```jsx
useSelector()
```

subscribe to selected store data.

If the selected result changes according to the selector's equality behavior, the component can re-render.

Avoid selecting a huge object when only a small piece is needed.

Prefer:

```jsx
const cart = useSelector(state => state.cart.items);
```

when that's all the component needs.

---

## 📌 52. How can Redux selectors improve performance?

Use focused selectors.

Instead of:

```jsx
const state = useSelector(state => state);
```

prefer:

```jsx
const user = useSelector(state => state.auth.user);
```

This reduces unnecessary subscriptions to unrelated state changes.

---

# 📌 Caching

## 📌 53. How does caching improve performance?

Caching avoids repeatedly downloading or calculating the same data.

Examples:

```text
Browser Cache
API Cache
CDN Cache
Server Cache
Database Cache
```

For MERN applications, Redis can also be used for suitable server-side caching scenarios.

---

# 📌 React Performance in MERN

## 📌 54. How would you optimize a MERN e-commerce application?

Suppose you have:

```text
React
   ↓
Node.js/Express
   ↓
MongoDB
```

Possible optimizations:

### Frontend

* Pagination
* Lazy loading
* Image optimization
* `React.memo` where useful
* Debounced search
* Virtualization for very large lists

### Backend

* Database indexes
* Efficient queries
* Pagination
* Caching
* Compression
* Proper API response sizes

### Network

* CDN
* HTTP caching
* Smaller JSON responses
* Keep API requests focused

---

## 📌 55. How would you optimize a product search page?

Example:

```text
Search Input
     ↓
Debounce
     ↓
API Request
     ↓
Pagination
     ↓
Render Products
```

Additional optimizations:

```text
Images → optimized
API → cached where appropriate
Products → pagination/virtualization if needed
Components → memoized selectively
```

---

# 📌 Common Mistakes

## 📌 56. What are common React performance mistakes?

### Mistake 1

Using `useMemo` everywhere.

### Mistake 2

Using `useCallback` everywhere.

### Mistake 3

Putting all state into Redux.

### Mistake 4

Rendering thousands of DOM nodes.

### Mistake 5

Using huge images.

### Mistake 6

Making an API request on every keystroke.

### Mistake 7

Using unstable keys.

### Mistake 8

Storing derived data unnecessarily.

### Mistake 9

Optimizing without measuring.

---

# 🎯 Top React Performance Interview Questions

## Q1. What is React.memo?

A performance optimization that allows React to skip rendering a component when its props are unchanged according to the memo comparison.

---

## Q2. What is useMemo?

It memoizes a calculated value.

```jsx
const value = useMemo(() => expensiveWork(data), [data]);
```

---

## Q3. What is useCallback?

It memoizes a function reference.

```jsx
const fn = useCallback(() => {
  doSomething();
}, []);
```

---

## Q4. useMemo vs useCallback?

```text
useMemo     → memoizes value
useCallback → memoizes function
```

---

## Q5. Does React.memo prevent all re-renders?

No.

A memoized component can still re-render because of:

* Its own state
* Context changes it consumes
* Changed props
* Other React/runtime conditions

---

## Q6. Why should we not use array indexes as keys?

Because indexes can change when list items are inserted, deleted, or reordered, causing incorrect component identity and potentially inefficient reconciliation.

---

## Q7. What is code splitting?

Breaking application code into smaller chunks so users don't have to download all JavaScript upfront.

---

## Q8. What is lazy loading?

Loading a resource/component only when it is needed.

---

## Q9. What is virtualization?

Rendering only the visible portion of a large list instead of creating DOM nodes for every item.

---

## Q10. How do you optimize a React application?

A strong interview answer:

> First I measure the performance problem using React Profiler and browser tools. Then I optimize the actual bottleneck using techniques such as reducing unnecessary renders, colocating state, memoizing expensive work where appropriate, splitting large bundles, lazy loading routes, optimizing images, debouncing requests, pagination or virtualization for large lists, and improving API/database performance.

---

# 🚀 Quick Revision

```text
React Performance
│
├── Rendering
│   ├── Avoid unnecessary renders
│   ├── React.memo
│   ├── State colocation
│   └── Stable keys
│
├── Memoization
│   ├── useMemo → value
│   └── useCallback → function
│
├── Large Data
│   ├── Pagination
│   ├── Infinite scroll
│   └── Virtualization
│
├── Loading
│   ├── React.lazy
│   ├── Suspense
│   └── Code splitting
│
├── Network
│   ├── Caching
│   ├── Debouncing
│   ├── Throttling
│   └── Request cancellation
│
├── Assets
│   ├── Image compression
│   ├── WebP/AVIF
│   └── Lazy loading
│
├── State
│   ├── Local state
│   ├── Context optimization
│   └── Redux selectors
│
└── Measurement
    ├── React Profiler
    ├── Chrome DevTools
    └── Core Web Vitals
```

# ⭐ Interview Formula

For almost any React performance question, remember:

```text
Measure
   ↓
Find bottleneck
   ↓
Reduce unnecessary work
   ↓
Optimize rendering/network/assets
   ↓
Measure again
```

> **Don't optimize everything. Optimize what measurement shows is actually slow.**
