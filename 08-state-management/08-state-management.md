# ⚛️ React State Management — Interview Questions & Answers

State management is one of the most important React interview topics, especially for **MERN Stack Developer** roles.

This file covers:

* Local State
* Lifting State Up
* Prop Drilling
* Context API
* Redux
* Redux Toolkit
* Store, Actions, Reducers, Dispatch
* `useSelector` & `useDispatch`
* Async Redux
* Global State
* Client State vs Server State
* State Architecture
* MERN Project Examples

---

## 📚 Table of Contents

1. [What is State Management?](#1-what-is-state-management)
2. [What is Local State?](#2-what-is-local-state)
3. [What is Global State?](#3-what-is-global-state)
4. [When Should State Be Global?](#4-when-should-state-be-global)
5. [What is Lifting State Up?](#5-what-is-lifting-state-up)
6. [What is Prop Drilling?](#6-what-is-prop-drilling)
7. [How Can Prop Drilling Be Solved?](#7-how-can-prop-drilling-be-solved)
8. [What is Context API?](#8-what-is-context-api)
9. [How Does Context API Work?](#9-how-does-context-api-work)
10. [Context API vs Redux](#10-context-api-vs-redux)
11. [What is Redux?](#11-what-is-redux)
12. [Why Use Redux?](#12-why-use-redux)
13. [Core Concepts of Redux](#13-core-concepts-of-redux)
14. [What is a Redux Store?](#14-what-is-a-redux-store)
15. [What is an Action?](#15-what-is-an-action)
16. [What is a Reducer?](#16-what-is-a-reducer)
17. [What is Dispatch?](#17-what-is-dispatch)
18. [What is a Selector?](#18-what-is-a-selector)
19. [Redux Data Flow](#19-redux-data-flow)
20. [What is Redux Toolkit?](#20-what-is-redux-toolkit)
21. [Why Redux Toolkit?](#21-why-redux-toolkit)
22. [What is `configureStore`?](#22-what-is-configurestore)
23. [What is `createSlice`?](#23-what-is-createslice)
24. [What is Provider?](#24-what-is-provider)
25. [What is `useSelector`?](#25-what-is-useselector)
26. [What is `useDispatch`?](#26-what-is-usedispatch)
27. [Redux Example](#27-redux-example)
28. [What is Immer in Redux Toolkit?](#28-what-is-immer-in-redux-toolkit)
29. [Can Redux Reducers Mutate State?](#29-can-redux-reducers-mutate-state)
30. [What is Middleware?](#30-what-is-middleware)
31. [What is Redux Thunk?](#31-what-is-redux-thunk)
32. [What is `createAsyncThunk`?](#32-what-is-createasyncthunk)
33. [Handling API Requests in Redux](#33-handling-api-requests-in-redux)
34. [Redux Loading and Error State](#34-redux-loading-and-error-state)
35. [Redux vs Local State](#35-redux-vs-local-state)
36. [Redux vs Context API](#36-redux-vs-context-api)
37. [Redux vs Zustand](#37-redux-vs-zustand)
38. [What is Client State?](#38-what-is-client-state)
39. [What is Server State?](#39-what-is-server-state)
40. [Should API Data Be Stored in Redux?](#40-should-api-data-be-stored-in-redux)
41. [What is Derived State?](#41-what-is-derived-state)
42. [Why Avoid Unnecessary Global State?](#42-why-avoid-unnecessary-global-state)
43. [How to Manage Authentication State?](#43-how-to-manage-authentication-state)
44. [How to Manage Cart State?](#44-how-to-manage-cart-state)
45. [How to Persist Redux State?](#45-how-to-persist-redux-state)
46. [Redux State Normalization](#46-redux-state-normalization)
47. [What Should Not Be Stored in Redux?](#47-what-should-not-be-stored-in-redux)
48. [How Does Redux Prevent Unnecessary Rendering?](#48-how-does-redux-prevent-unnecessary-rendering)
49. [Redux Architecture in MERN](#49-redux-architecture-in-mern)
50. [Interview Questions — Quick Revision](#50-interview-questions--quick-revision)

---

# 1. What is State Management?

State management means controlling and organizing the **data that can change over time** in an application.

Examples:

```text
User login status
Shopping cart
Products
Theme
Modal visibility
Search filters
Form data
Notifications
```

In React, state can be managed using:

```text
useState
useReducer
Context API
Redux Toolkit
Zustand
Server-state libraries
```

---

# 2. What is Local State?

Local state belongs to a particular component or a small component tree.

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

Here, `count` is local state.

### Examples

```text
Modal open/close
Input value
Dropdown state
Loading state for one component
Selected tab
```

If other components do not need the data, keep it local.

---

# 3. What is Global State?

Global state is state that can be accessed by multiple unrelated components.

Examples:

```text
Logged-in user
Authentication status
Shopping cart
Application theme
Notifications
Permissions
```

For example:

```text
Navbar
   ↓
User information

Product Page
   ↓
Add product to cart

Cart Page
   ↓
Same cart information
```

A shared store can prevent unnecessary prop passing between unrelated components.

---

# 4. When Should State Be Global?

Do **not** make every state global.

A state should usually become shared/global when:

* Multiple distant components need it.
* Many components need to update it.
* Prop drilling becomes excessive.
* State logic becomes complex.
* State must be accessed across multiple routes.

Example:

```text
Authentication → Global

Shopping Cart → Global

Modal used by one page → Local

Input field → Local
```

### Interview Answer

> I keep state local by default and move it to a shared solution only when multiple components genuinely need it.

---

# 5. What is Lifting State Up?

Lifting state up means moving shared state to the **nearest common parent** of the components that need it.

Example:

```text
        Parent
       /      \
   Child A   Child B
```

If both children need the same state:

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <ChildA count={count} />
      <ChildB setCount={setCount} />
    </>
  );
}
```

Now the parent owns the state.

---

# 6. What is Prop Drilling?

Prop drilling happens when data is passed through multiple components even though intermediate components don't use it.

Example:

```text
App
 ↓
Navbar
 ↓
UserMenu
 ↓
Profile
```

Suppose `Profile` needs `user`.

You may end up doing:

```jsx
<App user={user}>
  <Navbar user={user}>
    <UserMenu user={user}>
      <Profile user={user} />
    </UserMenu>
  </Navbar>
</App>
```

`Navbar` and `UserMenu` may not actually need `user`.

This is prop drilling.

---

# 7. How Can Prop Drilling Be Solved?

Common solutions:

```text
1. Component composition
2. Context API
3. Redux
4. Zustand
5. Other state-management libraries
```

Choose the simplest solution that fits the problem.

---

# 8. What is Context API?

Context API allows data to be shared with components without manually passing props through every intermediate component.

Example:

```jsx
const UserContext = createContext();
```

Then:

```jsx
<UserContext.Provider value={user}>
  <App />
</UserContext.Provider>
```

A child can consume it:

```jsx
const user = useContext(UserContext);
```

---

# 9. How Does Context API Work?

There are three important parts:

```text
createContext()
      ↓
Provider
      ↓
Consumer / useContext()
```

Example:

```jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext();

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Home />
    </ThemeContext.Provider>
  );
}

function Home() {
  const theme = useContext(ThemeContext);

  return <h1>{theme}</h1>;
}
```

Output:

```text
dark
```

---

# 10. Context API vs Redux

| Context API                         | Redux                             |
| ----------------------------------- | --------------------------------- |
| Built into React                    | External state library            |
| Simple                              | More structured                   |
| Good for shared values              | Good for complex global state     |
| Less boilerplate                    | Redux Toolkit reduces boilerplate |
| No built-in middleware architecture | Middleware support                |
| Good for theme/auth dependencies    | Good for complex app state        |

### Important

Context is **not automatically a replacement for Redux**.

Context primarily solves **prop passing/dependency sharing**. You can combine Context with `useState` or `useReducer` when appropriate.

---

# 11. What is Redux?

Redux is a predictable state management library used to manage shared application state.

Basic architecture:

```text
Components
    ↓
 dispatch(action)
    ↓
  Reducer
    ↓
  Store
    ↓
New State
    ↓
Components
```

Redux is especially useful when application state becomes complex and many components need to access or update it.

---

# 12. Why Use Redux?

Redux can provide:

* Centralized state
* Predictable state updates
* Clear data flow
* DevTools support
* Middleware
* Structured state logic
* Easier debugging

Example:

```text
User
Cart
Products
Notifications
Permissions
```

can be organized in one application store.

---

# 13. Core Concepts of Redux

The main Redux concepts are:

```text
Store
Action
Reducer
Dispatch
Selector
Middleware
```

Think of it like:

```text
Action
  ↓
Dispatch
  ↓
Reducer
  ↓
Store
  ↓
Updated UI
```

---

# 14. What is a Redux Store?

The store contains the application's Redux state.

Example:

```js
{
  auth: {
    user: null,
    isAuthenticated: false
  },

  cart: {
    items: []
  },

  products: {
    data: [],
    loading: false
  }
}
```

Modern Redux applications commonly create the store with:

```js
configureStore()
```

---

# 15. What is an Action?

An action describes **what happened**.

Example:

```js
{
  type: "cart/addItem",
  payload: product
}
```

An action should generally be a plain serializable object.

---

# 16. What is a Reducer?

A reducer determines how state changes in response to an action.

Conceptually:

```text
Previous State
      +
    Action
      ↓
    Reducer
      ↓
  New State
```

Example:

```js
function counterReducer(state, action) {
  if (action.type === "increment") {
    return state + 1;
  }

  return state;
}
```

Reducers should be predictable and free of side effects.

---

# 17. What is Dispatch?

`dispatch()` sends an action to the Redux store.

Example:

```jsx
dispatch(increment());
```

Flow:

```text
Button click
   ↓
dispatch()
   ↓
Action
   ↓
Reducer
   ↓
Store update
   ↓
UI update
```

---

# 18. What is a Selector?

A selector reads data from the Redux store.

Example:

```js
const cartItems = useSelector(
  state => state.cart.items
);
```

Selectors are useful because components don't need to know the complete store structure.

---

# 19. Redux Data Flow

Redux follows a predictable one-way data flow:

```text
User Interaction
      ↓
dispatch(action)
      ↓
Middleware (if any)
      ↓
Reducer
      ↓
Store
      ↓
Selector
      ↓
React Component
      ↓
UI
```

Example:

```text
Click "Add to Cart"
        ↓
dispatch(addItem(product))
        ↓
cartReducer
        ↓
cart.items updated
        ↓
Cart component re-renders
```

---

# 20. What is Redux Toolkit?

Redux Toolkit, commonly abbreviated as **RTK**, is the recommended way to write Redux logic.

It provides utilities such as:

```text
configureStore()
createSlice()
createAsyncThunk()
createEntityAdapter()
```

It makes Redux easier and reduces boilerplate.

---

# 21. Why Redux Toolkit?

Traditional Redux could require:

```text
Action Types
Action Creators
Reducers
Constants
Switch statements
Store configuration
Middleware configuration
```

Redux Toolkit simplifies this.

For example:

```js
const counterSlice = createSlice({
  name: "counter",

  initialState: {
    value: 0
  },

  reducers: {
    increment: state => {
      state.value++;
    }
  }
});
```

Much less boilerplate.

---

# 22. What is `configureStore`?

`configureStore()` creates the Redux store with useful defaults.

Example:

```js
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "./counterSlice";

export const store = configureStore({
  reducer: {
    counter: counterReducer
  }
});
```

It also sets up common middleware and development tooling defaults.

---

# 23. What is `createSlice`?

`createSlice()` combines:

```text
Initial state
Reducers
Action creators
Action types
```

Example:

```js
import { createSlice } from "@reduxjs/toolkit";

const cartSlice = createSlice({
  name: "cart",

  initialState: {
    items: []
  },

  reducers: {
    addItem: (state, action) => {
      state.items.push(action.payload);
    },

    removeItem: (state, action) => {
      state.items = state.items.filter(
        item => item.id !== action.payload
      );
    }
  }
});

export const {
  addItem,
  removeItem
} = cartSlice.actions;

export default cartSlice.reducer;
```

---

# 24. What is Provider?

`Provider` makes the Redux store available to React components below it.

Usually:

```jsx
import { Provider } from "react-redux";
import { store } from "./store";

createRoot(document.getElementById("root")).render(
  <Provider store={store}>
    <App />
  </Provider>
);
```

Without `Provider`, components cannot use React-Redux hooks against that store.

---

# 25. What is `useSelector`?

`useSelector()` reads data from the Redux store.

Example:

```jsx
const count = useSelector(
  state => state.counter.value
);
```

When the selected result changes according to React-Redux's comparison behavior, the component can re-render.

---

# 26. What is `useDispatch`?

`useDispatch()` gives access to the Redux store's `dispatch` function.

Example:

```jsx
const dispatch = useDispatch();

dispatch(increment());
```

With payload:

```jsx
dispatch(addItem(product));
```

---

# 27. Redux Example

### Store

```js
// store.js

import { configureStore } from "@reduxjs/toolkit";
import cartReducer from "./cartSlice";

export const store = configureStore({
  reducer: {
    cart: cartReducer
  }
});
```

### Slice

```js
// cartSlice.js

import { createSlice } from "@reduxjs/toolkit";

const cartSlice = createSlice({
  name: "cart",

  initialState: {
    items: []
  },

  reducers: {
    addItem: (state, action) => {
      state.items.push(action.payload);
    },

    removeItem: (state, action) => {
      state.items = state.items.filter(
        item => item.id !== action.payload
      );
    }
  }
});

export const { addItem, removeItem } =
  cartSlice.actions;

export default cartSlice.reducer;
```

### Component

```jsx
import { useDispatch, useSelector } from "react-redux";
import { addItem } from "./cartSlice";

function Product({ product }) {
  const dispatch = useDispatch();

  const items = useSelector(
    state => state.cart.items
  );

  return (
    <div>
      <button
        onClick={() => dispatch(addItem(product))}
      >
        Add to Cart
      </button>

      <p>Items: {items.length}</p>
    </div>
  );
}
```

---

# 28. What is Immer in Redux Toolkit?

Redux Toolkit uses **Immer** internally for reducers.

Immer allows developers to write code that looks like direct mutation:

```js
state.items.push(product);
```

while producing the necessary immutable state updates internally.

This does **not** mean Redux state is actually mutated directly.

---

# 29. Can Redux Reducers Mutate State?

In traditional Redux reducers, state should not be mutated directly.

Bad:

```js
state.count++;
return state;
```

With Redux Toolkit:

```js
increment: state => {
  state.count++;
}
```

is valid because Redux Toolkit uses Immer to translate these apparent mutations into immutable updates.

### Interview Trap

If the interviewer asks:

> Does Redux Toolkit allow mutation?

Answer:

> Redux Toolkit allows mutation-like syntax in reducers because Immer tracks those changes and produces a new immutable state internally.

---

# 30. What is Middleware?

Middleware runs between dispatching an action and the reducer processing it.

Conceptually:

```text
dispatch(action)
      ↓
 middleware
      ↓
 reducer
```

Middleware can be used for:

```text
Logging
Async operations
Analytics
Error reporting
Side effects
```

---

# 31. What is Redux Thunk?

Thunk middleware allows action dispatching to handle asynchronous logic.

For example:

```text
Component
   ↓
dispatch(fetchProducts())
   ↓
API request
   ↓
Response
   ↓
dispatch success/failure
```

Redux Toolkit's `configureStore` includes thunk middleware by default.

---

# 32. What is `createAsyncThunk`?

`createAsyncThunk()` is a Redux Toolkit helper for common asynchronous workflows.

Example:

```js
import {
  createAsyncThunk
} from "@reduxjs/toolkit";

export const fetchProducts =
  createAsyncThunk(
    "products/fetchProducts",
    async () => {
      const response =
        await fetch("/api/products");

      return await response.json();
    }
  );
```

It automatically generates lifecycle actions:

```text
pending
fulfilled
rejected
```

---

# 33. Handling API Requests in Redux

Example:

```js
const productsSlice = createSlice({
  name: "products",

  initialState: {
    data: [],
    loading: false,
    error: null
  },

  reducers: {},

  extraReducers: builder => {
    builder
      .addCase(
        fetchProducts.pending,
        state => {
          state.loading = true;
          state.error = null;
        }
      )

      .addCase(
        fetchProducts.fulfilled,
        (state, action) => {
          state.loading = false;
          state.data = action.payload;
        }
      )

      .addCase(
        fetchProducts.rejected,
        (state, action) => {
          state.loading = false;
          state.error =
            action.error.message;
        }
      );
  }
});
```

---

# 34. Redux Loading and Error State

For API calls, a common pattern is:

```js
{
  data: [],
  loading: false,
  error: null
}
```

During request:

```text
loading = true
```

Success:

```text
loading = false
error = null
```

Failure:

```text
loading = false
error = message
```

This gives the UI clear states:

```text
Loading...
    ↓
Success

OR

Loading...
    ↓
Error
```

---

# 35. Redux vs Local State

| Local State        | Redux                           |
| ------------------ | ------------------------------- |
| Component-specific | Shared application state        |
| Simple             | More structured                 |
| `useState`         | Redux Toolkit                   |
| Easy to create     | Better for complex shared state |
| Good for UI state  | Good for cross-component state  |

Example:

```text
Modal → useState

Input → useState

Cart → Redux

Authentication → Redux/Context depending on architecture
```

---

# 36. Redux vs Context API

### Context

Good for:

```text
Theme
Locale
Current user/dependency values
Small shared state
```

### Redux

Good for:

```text
Large application state
Complex state transitions
Many components
Middleware
Debugging
Structured global state
```

Do not choose Redux simply because an application has multiple components.

Choose based on complexity and sharing requirements.

---

# 37. Redux vs Zustand

Both can manage shared client state.

| Redux Toolkit             | Zustand                 |
| ------------------------- | ----------------------- |
| More structured           | Simpler API             |
| Strong conventions        | Less boilerplate        |
| Large ecosystem           | Lightweight             |
| Middleware support        | Middleware support      |
| Good for large teams/apps | Good for simpler stores |
| More concepts             | Fewer concepts          |

Interview answer:

> Redux Toolkit is useful when I want a structured and predictable state architecture, while Zustand can be attractive when I need a simpler external store with less boilerplate.

---

# 38. What is Client State?

Client state is state primarily controlled by the frontend application.

Examples:

```text
Modal visibility
Selected tab
Theme
Sidebar status
Shopping cart UI state
Authentication UI state
Filters
```

Example:

```js
const [isModalOpen, setIsModalOpen] =
  useState(false);
```

---

# 39. What is Server State?

Server state is data that originates from and is controlled by a backend/server.

Examples:

```text
Products
Users
Orders
Campaigns
Comments
Complaints
```

It usually involves:

```text
Fetching
Caching
Refetching
Synchronization
Loading
Errors
Stale data
```

Server state has different requirements from ordinary UI state.

---

# 40. Should API Data Be Stored in Redux?

It depends.

For simple applications, Redux can store API data:

```text
products
users
orders
```

But server-state-specific tools can be a better fit when an application needs sophisticated:

```text
Caching
Refetching
Invalidation
Request deduplication
Synchronization
```

The important interview point is:

> Not every piece of application data needs to be placed in Redux.

---

# 41. What is Derived State?

Derived state is data that can be calculated from existing state.

Example:

```js
const total = items.reduce(
  (sum, item) =>
    sum + item.price * item.quantity,
  0
);
```

You generally don't need:

```js
const [total, setTotal] = useState(0);
```

because `total` can be derived from `items`.

### Rule

> Store the minimum source state necessary and derive the rest.

---

# 42. Why Avoid Unnecessary Global State?

Making everything global can cause:

```text
Complex architecture
Harder debugging
Unnecessary subscriptions
Tighter coupling
More difficult testing
More difficult reasoning
```

For example:

```text
Search input
```

usually does not need to be in Redux if only one page uses it.

Prefer:

```jsx
const [search, setSearch] = useState("");
```

---

# 43. How to Manage Authentication State?

A typical MERN application may have:

```text
Authentication
      ↓
Backend
      ↓
JWT/session
      ↓
Frontend
      ↓
User state
```

Redux might hold information such as:

```js
{
  user: {
    id: "...",
    name: "Anurag"
  },
  isAuthenticated: true
}
```

Sensitive credentials should be handled according to the application's security architecture. For browser sessions, **HttpOnly, Secure cookies** can be preferable to exposing tokens to JavaScript, depending on the backend design.

---

# 44. How to Manage Cart State?

An e-commerce application can have:

```js
{
  cart: {
    items: [
      {
        id: 1,
        name: "Book",
        price: 500,
        quantity: 2
      }
    ]
  }
}
```

Actions:

```text
addItem
removeItem
increaseQuantity
decreaseQuantity
clearCart
```

Example:

```js
dispatch(addItem(product));
```

This allows:

```text
Product Page
      ↓
     Cart
      ↓
Cart Page
      ↓
Checkout
```

to share the same cart state.

---

# 45. How to Persist Redux State?

Redux state normally exists in memory.

A page refresh can therefore reset it unless state is persisted or reconstructed.

Possible approaches:

```text
1. localStorage
2. sessionStorage
3. Persisted Redux state libraries
4. Refetching from backend
5. HttpOnly cookies for session/auth mechanisms
```

For example, cart data could be persisted to `localStorage`.

However, don't blindly persist sensitive information.

---

# 46. Redux State Normalization

Normalization means structuring related data to avoid unnecessary duplication.

Instead of:

```js
users: [
  {
    id: 1,
    name: "Anurag",
    posts: [...]
  }
]
```

you can normalize:

```js
users: {
  byId: {
    1: {
      id: 1,
      name: "Anurag"
    }
  },

  allIds: [1]
}
```

This can make updates and lookups more efficient for complex relational data.

Redux Toolkit provides:

```js
createEntityAdapter()
```

to help with normalized collections.

---

# 47. What Should Not Be Stored in Redux?

Avoid storing things that don't need to be shared globally.

Examples:

```text
Temporary input values
Local modal state
DOM nodes
Promises
Non-serializable class instances
Functions
Large temporary objects
Derived values
```

Redux state is best kept predictable and serializable where practical.

---

# 48. How Does Redux Prevent Unnecessary Rendering?

React-Redux subscribes components to the store.

For example:

```jsx
const user = useSelector(
  state => state.auth.user
);
```

The component is interested in the selected value.

If unrelated parts of the store change, the component does not automatically need to re-render merely because the store changed.

However, selectors should be written carefully because returning a newly created object/array on every call can affect equality checks.

---

# 49. Redux Architecture in MERN

A practical MERN architecture could look like:

```text
                 React
                   │
        ┌──────────┴──────────┐
        │                     │
      Pages              Components
        │                     │
        └──────────┬──────────┘
                   ↓
             Redux Toolkit
                   │
        ┌──────────┼──────────┐
        ↓          ↓          ↓
      Auth       Cart      Products
        │          │          │
        └──────────┼──────────┘
                   ↓
                API
                   ↓
              Express.js
                   ↓
              Controllers
                   ↓
              MongoDB
```

Example Redux folders:

```text
src/
│
├── app/
│   └── store.js
│
├── features/
│   ├── auth/
│   │   ├── authSlice.js
│   │   └── authApi.js
│   │
│   ├── cart/
│   │   └── cartSlice.js
│   │
│   └── products/
│       ├── productsSlice.js
│       └── productsApi.js
│
├── components/
├── pages/
└── App.jsx
```

---

# 50. Interview Questions — Quick Revision

## ⭐ Basic

### 1. What is state management?

Managing changing application data and ensuring components receive the correct updated values.

### 2. What is local state?

State owned by a component or small component tree.

### 3. What is global state?

Shared state accessible by multiple unrelated parts of an application.

### 4. What is lifting state up?

Moving state to the nearest common parent of components that need it.

### 5. What is prop drilling?

Passing props through intermediate components that don't need the data themselves.

### 6. What is Context API?

A React mechanism for sharing values through a component tree without manually passing props at every level.

---

## ⭐ Redux

### 7. What is Redux?

A predictable state management library for managing shared application state.

### 8. What are Redux's core concepts?

```text
Store
Action
Reducer
Dispatch
Selector
Middleware
```

### 9. What is an action?

A serializable object describing what happened.

### 10. What is a reducer?

A function that determines the next state from the current state and an action.

### 11. What is dispatch?

The mechanism used to send an action to Redux.

### 12. What is a selector?

A function used to read data from the Redux store.

---

## ⭐ Redux Toolkit

### 13. What is Redux Toolkit?

The recommended modern approach for writing Redux logic.

### 14. What is `createSlice()`?

A utility that generates reducers and corresponding action creators/action types from a slice definition.

### 15. What is `configureStore()`?

A utility for creating and configuring the Redux store with useful defaults.

### 16. What is `useSelector()`?

A React-Redux hook for reading selected data from the store.

### 17. What is `useDispatch()`?

A React-Redux hook that provides the dispatch function.

### 18. Why can we write `state.count++` in Redux Toolkit?

Because Redux Toolkit uses Immer to produce immutable state updates from mutation-like reducer code.

---

## ⭐ Advanced

### 19. What is middleware?

Logic that runs between dispatching an action and reducer processing.

### 20. What is Redux Thunk?

Middleware that enables dispatching functions for asynchronous workflows.

### 21. What is `createAsyncThunk()`?

A Redux Toolkit helper for common async request lifecycles.

### 22. What are `pending`, `fulfilled`, and `rejected`?

They represent the common lifecycle states of an async thunk.

### 23. What is derived state?

Data calculated from existing state rather than independently stored.

### 24. What is state normalization?

Structuring related entities to reduce duplication and simplify updates/lookups.

### 25. Should everything be stored in Redux?

No. Keep state local unless it genuinely needs to be shared or managed centrally.

---

# 🎯 Most Important Interview Questions

If you have limited preparation time, focus on these:

```text
1. What is state management?
2. Local state vs global state
3. What is lifting state up?
4. What is prop drilling?
5. Context API
6. Context API vs Redux
7. What is Redux?
8. Redux data flow
9. Store
10. Action
11. Reducer
12. Dispatch
13. Selector
14. Redux Toolkit
15. createSlice()
16. configureStore()
17. Provider
18. useSelector()
19. useDispatch()
20. Immer
21. Middleware
22. Redux Thunk
23. createAsyncThunk()
24. Loading/error states
25. Redux vs Context
26. Redux vs Zustand
27. Client state vs server state
28. Derived state
29. State normalization
30. How to manage authentication/cart state
```

---

# 🧠 One-Minute Redux Revision

Remember:

```text
STORE
 ↓
Contains application state

ACTION
 ↓
Describes what happened

DISPATCH
 ↓
Sends the action

REDUCER
 ↓
Calculates the next state

SELECTOR
 ↓
Reads state

COMPONENT
 ↓
Displays UI
```

Modern Redux:

```text
Redux
  ↓
Redux Toolkit
  ↓
createSlice()
configureStore()
createAsyncThunk()
useSelector()
useDispatch()
```

---

# 🚀 MERN Interview Example

### Interviewer:

> How would you manage a shopping cart in your MERN application?

### Strong Answer:

> I would first keep the cart local if it is only required by a small component tree. If multiple pages such as the product page, navbar, cart page, and checkout page need the same cart state, I would use shared state such as Redux Toolkit. I would create a cart slice containing actions such as `addItem`, `removeItem`, and `updateQuantity`. The cart UI would use `useSelector` to read the cart and `useDispatch` to update it. If the cart needs backend persistence, I would synchronize it with the Express API and MongoDB.

---

# 🚀 Another MERN Interview Example

### Interviewer:

> Where would you store product search input?

Good answer:

```text
Local state
```

Example:

```jsx
const [search, setSearch] = useState("");
```

If the search state needs to be shared across many unrelated parts of the application, then a shared state solution may be justified.

---

# 💡 Golden Rule

> **Keep state as local as possible and make it global only when there is a real sharing or coordination requirement.**

A good state architecture is not about putting everything into Redux.

It is about putting **each piece of state in the simplest place that correctly serves the application.**

---

## 🔥 Interview Formula

When asked:

> "Which state management approach would you use?"

Answer:

```text
Small/local state
      ↓
useState

Complex local state
      ↓
useReducer

Shared simple values
      ↓
Context API

Complex shared client state
      ↓
Redux Toolkit / another external store

Server state
      ↓
Server-state/data-fetching solution when appropriate
```

This demonstrates that you understand **state architecture**, rather than simply knowing Redux syntax.
