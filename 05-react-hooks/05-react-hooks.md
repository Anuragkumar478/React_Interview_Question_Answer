# ⚛️ React Hooks — Interview Questions & Answers

A complete collection of **React Hooks interview questions and answers**, from beginner to advanced level.

---

## 📚 Table of Contents

1. [What are Hooks?](#1-what-are-hooks)
2. [Why were Hooks introduced?](#2-why-were-hooks-introduced)
3. [What are the Rules of Hooks?](#3-what-are-the-rules-of-hooks)
4. [useState](#4-usestate)
5. [useEffect](#5-useeffect)
6. [useRef](#6-useref)
7. [useContext](#7-usecontext)
8. [useReducer](#8-usereducer)
9. [useMemo](#9-usememo)
10. [useCallback](#10-usecallback)
11. [useLayoutEffect](#11-uselayouteffect)
12. [useId](#12-useid)
13. [useTransition](#13-usetransition)
14. [useDeferredValue](#14-usedeferredvalue)
15. [Custom Hooks](#15-custom-hooks)
16. [Common Interview Questions](#16-common-interview-questions)
17. [MERN Project Examples](#17-mern-project-examples)
18. [Quick Revision](#18-quick-revision)

---

# 1. What are Hooks?

Hooks are special functions introduced in React that allow function components to use features such as:

* State
* Effects
* Context
* Refs
* Reducers
* Performance optimizations

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

---

# 2. Why were Hooks introduced?

Before Hooks, state and lifecycle logic were mainly associated with class components.

Hooks made it possible to:

* Use state in function components
* Reuse stateful logic
* Avoid class syntax
* Keep related logic together
* Create reusable custom hooks

---

# 3. What are the Rules of Hooks?

There are two major rules:

### Rule 1: Call Hooks only at the top level

Do not call Hooks inside:

* `if`
* `for`
* `while`
* nested functions
* callbacks

Bad:

```jsx
if (isLoggedIn) {
  const [user, setUser] = useState(null);
}
```

Good:

```jsx
const [user, setUser] = useState(null);

if (isLoggedIn) {
  // use user here
}
```

### Rule 2: Call Hooks only from React functions

Hooks can be called inside:

* Function components
* Custom Hooks

They should not be called from ordinary JavaScript functions.

---

# 4. What is `useState`?

`useState` is a Hook used to add state to a function component.

```jsx
const [count, setCount] = useState(0);
```

Here:

* `count` → current state
* `setCount` → state update function
* `0` → initial value

Example:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </>
  );
}
```

---

# 5. Can `useState` store objects?

Yes.

```jsx
const [user, setUser] = useState({
  name: "Anurag",
  age: 21
});
```

To update one property:

```jsx
setUser(prev => ({
  ...prev,
  age: 22
}));
```

We create a new object instead of directly modifying the existing state.

---

# 6. Can `useState` store arrays?

Yes.

```jsx
const [products, setProducts] = useState([]);
```

Add an item:

```jsx
setProducts(prev => [...prev, newProduct]);
```

Remove an item:

```jsx
setProducts(prev =>
  prev.filter(product => product.id !== id)
);
```

---

# 7. What is a functional state update?

A functional update receives the previous state.

```jsx
setCount(prev => prev + 1);
```

It is especially useful when the new state depends on the previous state.

Example:

```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

This correctly applies three increments.

---

# 8. Why should we use functional updates?

Because React may batch state updates.

Instead of depending on a potentially stale value:

```jsx
setCount(count + 1);
```

use:

```jsx
setCount(prev => prev + 1);
```

when the calculation depends on previous state.

---

# 9. Does updating state immediately change the variable?

No.

State updates schedule a new render.

```jsx
setCount(count + 1);

console.log(count);
```

The `console.log` still sees the value from the current render.

The updated state is available during the next render.

---

# 10. What is `useEffect`?

`useEffect` is used to synchronize a component with an **external system or side effect**.

Examples:

* API requests
* Timers
* Event listeners
* Subscriptions
* Browser APIs
* WebSocket connections

Example:

```jsx
import { useEffect } from "react";

useEffect(() => {
  console.log("Effect executed");
}, []);
```

---

# 11. What is the syntax of `useEffect`?

```jsx
useEffect(() => {
  // effect logic

  return () => {
    // cleanup
  };
}, [dependencies]);
```

The cleanup function is optional.

---

# 12. When does `useEffect` run?

Consider:

```jsx
useEffect(() => {
  console.log("Effect");
});
```

Without a dependency array, the effect re-synchronizes after every committed render.

---

# 13. What does an empty dependency array mean?

```jsx
useEffect(() => {
  console.log("Effect");
}, []);
```

It means the effect has no reactive dependencies.

In production, it normally runs after the initial mount.

However, in development with React Strict Mode, React may run the setup/cleanup cycle an extra time to help detect bugs.

So saying "`[]` means it always runs exactly once" is not completely accurate.

---

# 14. What does the dependency array do?

Example:

```jsx
useEffect(() => {
  console.log(userId);
}, [userId]);
```

The effect re-synchronizes when `userId` changes.

The dependency list should include the reactive values used by the effect that it depends on.

---

# 15. What is cleanup in `useEffect`?

Cleanup is a function returned from the effect.

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

* Clearing timers
* Removing event listeners
* Unsubscribing
* Closing connections
* Aborting requests

---

# 16. Why is cleanup important?

Without cleanup, resources can remain active after a component is removed.

For example:

```jsx
useEffect(() => {
  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

This prevents the listener from remaining attached unnecessarily.

---

# 17. How do you fetch API data using `useEffect`?

Example:

```jsx
import { useEffect, useState } from "react";

function Products() {
  const [products, setProducts] = useState([]);

  useEffect(() => {
    fetch("/api/products")
      .then(res => res.json())
      .then(data => setProducts(data));
  }, []);

  return (
    <div>
      {products.map(product => (
        <p key={product._id}>
          {product.name}
        </p>
      ))}
    </div>
  );
}
```

For production applications, also consider loading/error handling and cancellation or race-condition handling.

---

# 18. Should every API request be placed inside `useEffect`?

No.

`useEffect` is appropriate when fetching is part of synchronizing the component with external data.

But event-driven requests such as:

```jsx
const handleSubmit = async () => {
  await axios.post("/api/login", data);
};
```

can be triggered directly by the event handler.

Do not put every piece of application logic into `useEffect`.

---

# 19. What is an unnecessary useEffect?

If a value can be calculated directly from existing state/props, an effect is often unnecessary.

Bad:

```jsx
const [firstName, setFirstName] = useState("");
const [lastName, setLastName] = useState("");
const [fullName, setFullName] = useState("");

useEffect(() => {
  setFullName(`${firstName} ${lastName}`);
}, [firstName, lastName]);
```

Better:

```jsx
const fullName = `${firstName} ${lastName}`;
```

This is called **derived data**.

---

# 20. What is `useRef`?

`useRef` stores a mutable value that persists between renders without causing a re-render when changed.

```jsx
const ref = useRef(initialValue);
```

The value is stored in:

```jsx
ref.current
```

---

# 21. How is `useRef` used to access a DOM element?

```jsx
import { useRef } from "react";

function Input() {
  const inputRef = useRef(null);

  const focusInput = () => {
    inputRef.current.focus();
  };

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

---

# 22. Does changing `ref.current` cause a re-render?

No.

```jsx
const countRef = useRef(0);

countRef.current++;
```

Changing `ref.current` does not trigger a React render.

If the UI needs to update, use state.

---

# 23. `useState` vs `useRef`

| `useState`                  | `useRef`                               |
| --------------------------- | -------------------------------------- |
| Updating causes re-render   | Updating doesn't cause re-render       |
| Used for UI state           | Used for mutable values/DOM references |
| State updates are scheduled | `ref.current` changes immediately      |
| Value is part of rendering  | Value persists without rendering       |

---

# 24. What is `useContext`?

`useContext` allows a component to consume context without manually passing props through every intermediate component.

Example:

```jsx
const ThemeContext = createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Home />
    </ThemeContext.Provider>
  );
}
```

Consumer:

```jsx
function Home() {
  const theme = useContext(ThemeContext);

  return <div>{theme}</div>;
}
```

---

# 25. What problem does `useContext` solve?

It helps reduce **prop drilling**.

Without context:

```text
App
 ↓
Parent
 ↓
Child
 ↓
GrandChild
```

A value may need to be passed through components that do not actually use it.

Context allows a descendant to consume the value directly.

---

# 26. Does Context replace Redux or all state management?

No.

Context is primarily a way to make values available to a subtree.

It does not automatically provide all the features of dedicated state-management libraries.

For example:

* Context → theme/auth/configuration
* Redux/Zustand → complex shared client state
* React Query/TanStack Query → server-state management

The choice depends on the application.

---

# 27. What is `useReducer`?

`useReducer` is a Hook for managing state using a reducer function.

Syntax:

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

Example:

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return {
        count: state.count + 1
      };

    default:
      return state;
  }
}
```

Usage:

```jsx
const [state, dispatch] = useReducer(reducer, {
  count: 0
});

dispatch({ type: "increment" });
```

---

# 28. When should you use `useReducer`?

It is useful when:

* State is complex
* Multiple fields change together
* Many actions affect the same state
* State transitions need a clear structure

Example:

```text
idle
 ↓
loading
 ↓
success

or

loading
 ↓
error
```

---

# 29. `useState` vs `useReducer`

| useState              | useReducer                 |
| --------------------- | -------------------------- |
| Simple state          | Complex state              |
| Direct setter         | `dispatch(action)`         |
| Less boilerplate      | More structured            |
| Good for simple forms | Good for complex workflows |

---

# 30. What is `useMemo`?

`useMemo` memoizes the result of a calculation.

```jsx
const result = useMemo(() => {
  return expensiveCalculation(data);
}, [data]);
```

React can reuse the calculated value when dependencies have not changed.

---

# 31. Why is `useMemo` used?

It can optimize expensive calculations.

Example:

```jsx
const filteredProducts = useMemo(() => {
  return products.filter(product =>
    product.name
      .toLowerCase()
      .includes(search.toLowerCase())
  );
}, [products, search]);
```

---

# 32. Should `useMemo` be used everywhere?

No.

`useMemo` is a performance optimization, not something you need for every calculation.

For simple calculations:

```jsx
const total = price * quantity;
```

there is usually no reason to use:

```jsx
const total = useMemo(
  () => price * quantity,
  [price, quantity]
);
```

---

# 33. What is `useCallback`?

`useCallback` memoizes a function reference.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

This can help when function identity matters.

---

# 34. Why is `useCallback` useful with `React.memo`?

Consider:

```jsx
const Child = React.memo(function Child({ onClick }) {
  return <button onClick={onClick}>Click</button>;
});
```

If the parent creates a new function every render:

```jsx
const handleClick = () => {
  console.log("Click");
};
```

the child receives a new function reference.

Using:

```jsx
const handleClick = useCallback(() => {
  console.log("Click");
}, []);
```

can preserve the function reference between renders when dependencies do not change.

---

# 35. `useMemo` vs `useCallback`

Simple difference:

```text
useMemo     → memoizes a value
useCallback → memoizes a function
```

Example:

```jsx
const total = useMemo(() => price * quantity, [
  price,
  quantity
]);
```

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

---

# 36. Is `useCallback` always a performance improvement?

No.

It also has a cost and can make code more complicated.

Use it when function identity matters, such as:

* Passing a callback to a memoized child
* Using a function as a dependency where stable identity is useful
* Avoiding unnecessary work in specific cases

Do not blindly wrap every function in `useCallback`.

---

# 37. What is `useLayoutEffect`?

`useLayoutEffect` is similar to `useEffect`, but it runs after React has updated the DOM and before the browser paints.

It can be useful for:

* Measuring DOM elements
* Synchronously adjusting layout
* Avoiding visible layout jumps

Example:

```jsx
useLayoutEffect(() => {
  const width = elementRef.current.offsetWidth;
  console.log(width);
}, []);
```

---

# 38. `useEffect` vs `useLayoutEffect`

| useEffect                                | useLayoutEffect                      |
| ---------------------------------------- | ------------------------------------ |
| Runs after commit, generally after paint | Runs after DOM mutation before paint |
| Preferred for most effects               | Useful for layout-sensitive work     |
| Doesn't block paint in the same way      | Can block painting                   |
| Usually the default choice               | Use only when necessary              |

---

# 39. What is `useId`?

`useId` generates a stable unique ID suitable for associating elements such as labels and inputs.

Example:

```jsx
const id = useId();

return (
  <>
    <label htmlFor={id}>Email</label>
    <input id={id} />
  </>
);
```

It is particularly useful for accessibility and server/client rendering consistency.

---

# 40. Can `useId` be used as a list key?

No.

Do not use:

```jsx
items.map(item => (
  <div key={useId()}>
    {item.name}
  </div>
));
```

Use a stable data identifier instead:

```jsx
items.map(item => (
  <div key={item._id}>
    {item.name}
  </div>
));
```

---

# 41. What is `useTransition`?

`useTransition` lets you mark some state updates as non-urgent.

```jsx
const [isPending, startTransition] = useTransition();
```

Example:

```jsx
startTransition(() => {
  setSearchQuery(value);
});
```

React can keep urgent interactions responsive while handling the transition update.

---

# 42. When is `useTransition` useful?

It can be useful when an update causes expensive rendering.

For example:

```text
User types
     ↓
Input must stay responsive
     ↓
Large list filtering is less urgent
```

The expensive update can be marked as a transition.

---

# 43. What is `useDeferredValue`?

`useDeferredValue` allows a value to be treated as non-urgent.

```jsx
const deferredSearch = useDeferredValue(search);
```

You can use the deferred value for expensive UI.

Example:

```jsx
const filteredProducts = products.filter(product =>
  product.name.includes(deferredSearch)
);
```

The input can remain responsive while the expensive UI catches up.

---

# 44. `useTransition` vs `useDeferredValue`

| useTransition                                 | useDeferredValue                      |
| --------------------------------------------- | ------------------------------------- |
| Marks a state update as non-urgent            | Defers a value                        |
| You control the update with `startTransition` | React provides a deferred version     |
| Provides `isPending`                          | Does not provide the same pending API |

---

# 45. What are Custom Hooks?

Custom Hooks are reusable JavaScript functions that use React Hooks.

They normally start with:

```text
use
```

Examples:

```text
useAuth()
useFetch()
useDebounce()
useLocalStorage()
useCart()
```

---

# 46. Why use Custom Hooks?

Custom Hooks help extract and reuse stateful logic.

For example, instead of repeating authentication logic in several components:

```jsx
const { user, loading, logout } = useAuth();
```

Multiple components can reuse the same logic.

---

# 47. How do you create a custom Hook?

Example:

```jsx
import { useState } from "react";

function useCounter(initialValue = 0) {
  const [count, setCount] = useState(initialValue);

  const increment = () => {
    setCount(prev => prev + 1);
  };

  const decrement = () => {
    setCount(prev => prev - 1);
  };

  return {
    count,
    increment,
    decrement
  };
}
```

Usage:

```jsx
function Counter() {
  const {
    count,
    increment,
    decrement
  } = useCounter(0);

  return (
    <>
      <p>{count}</p>

      <button onClick={increment}>
        +
      </button>

      <button onClick={decrement}>
        -
      </button>
    </>
  );
}
```

---

# 48. Do Custom Hooks share state between components?

The logic is shared, but the state is **not automatically shared**.

For example:

```jsx
const counter1 = useCounter();
const counter2 = useCounter();
```

Each Hook call gets its own state.

If multiple components need the same state, you can use:

* Context
* A state-management library
* Lifted state
* Server-state tools

---

# 49. Why does Hook call order matter?

React relies on Hooks being called in the same order on every render.

Example:

```jsx
const [name, setName] = useState("");
const [age, setAge] = useState(20);
```

React internally associates the first Hook with the first state slot and the second Hook with the second slot.

If Hooks are conditionally called, the order can change and React can no longer reliably match state to Hooks.

That's why this is invalid:

```jsx
if (loggedIn) {
  useEffect(() => {});
}
```

---

# 50. Can Hooks be used inside loops?

No.

Bad:

```jsx
for (let i = 0; i < 5; i++) {
  useState(0);
}
```

Hooks must be called at the top level.

---

# 51. Can Hooks be used inside event handlers?

No.

Bad:

```jsx
function handleClick() {
  const [count, setCount] = useState(0);
}
```

Instead, declare the Hook at component level:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setCount(prev => prev + 1);
  };
}
```

---

# 52. Can Hooks be used inside a custom Hook?

Yes.

Example:

```jsx
function useUser() {
  const [user, setUser] = useState(null);

  useEffect(() => {
    // fetch user
  }, []);

  return user;
}
```

---

# 53. What is a stale closure in React?

A stale closure occurs when a function captures an older value from a previous render.

Example:

```jsx
useEffect(() => {
  const timer = setInterval(() => {
    console.log(count);
  }, 1000);

  return () => clearInterval(timer);
}, []);
```

The callback can keep referring to the value captured when the effect was created.

Solutions depend on the use case, such as:

* Correct dependencies
* Functional state updates
* Refs for mutable latest values

---

# 54. How can you avoid stale state when updating?

Use a functional update when the next state depends on previous state.

Instead of:

```jsx
setCount(count + 1);
```

use:

```jsx
setCount(prev => prev + 1);
```

This is especially important in callbacks, timers, and batched updates.

---

# 55. What happens when a component using Hooks unmounts?

React removes the component from the UI.

For effects, React runs the cleanup function when the effect needs to be cleaned up.

Example:

```jsx
useEffect(() => {
  const socket = connect();

  return () => {
    socket.disconnect();
  };
}, []);
```

This prevents resources from remaining active after unmount.

---

# 56. Can Hooks be used in class components?

No.

Hooks are designed for:

* Function components
* Custom Hooks

Class components use lifecycle methods and class state instead.

---

# 57. What is the difference between `useEffect` and event handlers?

An event handler responds to a specific user interaction.

```jsx
const handleSubmit = () => {
  login();
};
```

An effect synchronizes with something outside the component when its dependencies change.

```jsx
useEffect(() => {
  document.title = `Count: ${count}`;
}, [count]);
```

Use the right mechanism instead of putting everything inside `useEffect`.

---

# 58. How would you implement debounce with a custom Hook?

Example:

```jsx
import { useEffect, useState } from "react";

function useDebounce(value, delay = 500) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => {
      setDebouncedValue(value);
    }, delay);

    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}
```

Usage:

```jsx
const debouncedSearch = useDebounce(search, 500);
```

This is useful for search APIs.

---

# 59. How would you use Hooks in a MERN application?

Example:

```jsx
function Products() {
  const [products, setProducts] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const fetchProducts = async () => {
      try {
        const response = await axios.get("/api/products");
        setProducts(response.data);
      } finally {
        setLoading(false);
      }
    };

    fetchProducts();
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  return (
    <div>
      {products.map(product => (
        <ProductCard
          key={product._id}
          product={product}
        />
      ))}
    </div>
  );
}
```

Here:

```text
useState  → products/loading
useEffect → API synchronization
```

---

# 60. Which Hooks are most important for a React interview?

For a fresher/MERN interview, prioritize:

### Must Know

```text
useState
useEffect
useRef
useContext
useReducer
```

### Performance

```text
useMemo
useCallback
```

### Advanced

```text
useLayoutEffect
useId
useTransition
useDeferredValue
```

### Very Important Concept

```text
Custom Hooks
Rules of Hooks
Dependency arrays
Effect cleanup
Stale closures
```

---

# 61. Real MERN Example: Authentication Hook

A custom authentication Hook might look like:

```jsx
function useAuth() {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    const checkAuth = async () => {
      try {
        const response = await axios.get(
          "/api/auth/me",
          { withCredentials: true }
        );

        setUser(response.data.user);
      } catch (error) {
        setUser(null);
      } finally {
        setLoading(false);
      }
    };

    checkAuth();
  }, []);

  return {
    user,
    loading,
    isAuthenticated: !!user
  };
}
```

Usage:

```jsx
function Dashboard() {
  const {
    user,
    loading,
    isAuthenticated
  } = useAuth();

  if (loading) {
    return <p>Loading...</p>;
  }

  if (!isAuthenticated) {
    return <p>Please login</p>;
  }

  return <h1>Welcome {user.name}</h1>;
}
```

---

# 62. Real MERN Example: Cart Hook

```jsx
function useCart() {
  const [cart, setCart] = useState([]);

  const addToCart = product => {
    setCart(prev => [...prev, product]);
  };

  const removeFromCart = id => {
    setCart(prev =>
      prev.filter(item => item._id !== id)
    );
  };

  const total = useMemo(() => {
    return cart.reduce(
      (sum, item) => sum + item.price,
      0
    );
  }, [cart]);

  return {
    cart,
    addToCart,
    removeFromCart,
    total
  };
}
```

This combines:

```text
useState
useMemo
Custom Hook
```

---

# 63. Real MERN Example: Search Optimization

Suppose your application has thousands of products.

You can use:

```jsx
const [search, setSearch] = useState("");

const deferredSearch = useDeferredValue(search);
```

Then expensive filtering can use:

```jsx
const filteredProducts = products.filter(product =>
  product.name
    .toLowerCase()
    .includes(deferredSearch.toLowerCase())
);
```

This can help keep the typing interaction responsive.

---

# 64. What is the most common mistake with `useEffect`?

Putting too much application logic inside effects.

For example:

```jsx
useEffect(() => {
  setFullName(firstName + lastName);
}, [firstName, lastName]);
```

If `fullName` is simply derived from existing state, calculate it directly:

```jsx
const fullName = firstName + lastName;
```

Use effects primarily for synchronization with external systems.

---

# 65. What is the most common mistake with `useMemo` and `useCallback`?

Using them everywhere.

For example:

```jsx
const name = useMemo(() => user.name, [user]);
```

This usually provides no meaningful benefit.

The goal is not:

> "Use memoization everywhere."

The goal is:

> "Use memoization when it solves a measured or meaningful rendering/reference-identity problem."

---

# 66. What should you remember about Hooks in interviews?

Remember this structure:

```text
useState
   ↓
State

useEffect
   ↓
External synchronization / side effects

useRef
   ↓
Persistent mutable value / DOM reference

useContext
   ↓
Consume context

useReducer
   ↓
Complex state transitions

useMemo
   ↓
Memoized calculated value

useCallback
   ↓
Memoized function reference

Custom Hook
   ↓
Reusable stateful logic
```

---

# ⚡ Quick Revision

| Hook               | Main Purpose                          |
| ------------------ | ------------------------------------- |
| `useState`         | Component state                       |
| `useEffect`        | Synchronize with external systems     |
| `useRef`           | Mutable value / DOM reference         |
| `useContext`       | Consume context                       |
| `useReducer`       | Complex state transitions             |
| `useMemo`          | Memoize calculated value              |
| `useCallback`      | Memoize function reference            |
| `useLayoutEffect`  | Layout-sensitive effects before paint |
| `useId`            | Stable IDs                            |
| `useTransition`    | Mark updates as non-urgent            |
| `useDeferredValue` | Defer a value                         |
| Custom Hook        | Reusable stateful logic               |

---

# 🎯 Top 15 Hook Interview Questions

Before an interview, make sure you can answer these without looking at notes:

1. What are React Hooks?
2. Why were Hooks introduced?
3. What are the Rules of Hooks?
4. How does `useState` work?
5. Why use functional state updates?
6. What is `useEffect`?
7. Explain the dependency array.
8. What is effect cleanup?
9. Why can `useEffect` run more than once in development?
10. What is `useRef`?
11. `useState` vs `useRef`?
12. `useMemo` vs `useCallback`?
13. When should you use `useReducer`?
14. What are Custom Hooks?
15. Explain a Hook you used in your MERN project.

---

# 💼 Interview Formula

When the interviewer asks **"Which Hooks have you used?"**, don't just list them.

Answer with usage:

> "I have mainly used `useState` for component state, `useEffect` for API calls and external synchronization, `useRef` for DOM references and persistent mutable values, `useContext` for shared application values, and `useMemo`/`useCallback` when optimization or stable references were actually needed. I have also created custom Hooks to reuse logic such as authentication, fetching, and debouncing."

This demonstrates practical knowledge rather than only memorization.
