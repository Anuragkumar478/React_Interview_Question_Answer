# ⚛️ Props & State – React Interview Questions & Answers

> React interview preparation covering Props, State, state updates, immutability, batching, lifting state, derived state, and common interview traps.

---

# 📌 Part 1 — Props

## 1. What are Props in React?

Props, short for **properties**, are inputs passed from a parent component to a child component.

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

## 2. Why are Props used?

Props are mainly used to:

* Pass data between components
* Configure reusable components
* Pass callback functions
* Pass objects and arrays
* Pass React elements/components

Example:

```jsx
<Product
  name="Laptop"
  price={50000}
  inStock={true}
/>
```

The same `Product` component can display different products.

---

## 3. Are Props mutable?

No.

A child component should treat its props as **read-only**.

Incorrect:

```jsx
function User(props) {
  props.name = "Rahul";

  return <h1>{props.name}</h1>;
}
```

Instead, if the value needs to change, the state should be owned by an appropriate component.

---

## 4. Can Props contain functions?

Yes.

A very common pattern is passing a callback from parent to child.

```jsx
function Parent() {
  const handleClick = () => {
    console.log("Button clicked");
  };

  return <Child onClick={handleClick} />;
}

function Child({ onClick }) {
  return (
    <button onClick={onClick}>
      Click
    </button>
  );
}
```

Here `onClick` is a function prop.

---

## 5. Can Props contain objects and arrays?

Yes.

### Object

```jsx
const user = {
  name: "Anurag",
  age: 21
};

<User user={user} />
```

### Array

```jsx
const products = [
  { id: 1, name: "Book" },
  { id: 2, name: "Laptop" }
];

<ProductList products={products} />
```

---

## 6. What is destructuring Props?

Instead of:

```jsx
function User(props) {
  return <h1>{props.name}</h1>;
}
```

we can use destructuring:

```jsx
function User({ name }) {
  return <h1>{name}</h1>;
}
```

Multiple props:

```jsx
function User({ name, age, role }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>{age}</p>
      <p>{role}</p>
    </div>
  );
}
```

---

## 7. What is the `children` prop?

`children` represents the content placed between a component's opening and closing tags.

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

The content inside `Card` is available through `children`.

---

## 8. What is the difference between Props and HTML attributes?

They look similar but have different purposes.

HTML:

```html
<input type="text" />
```

React component:

```jsx
<User name="Anurag" />
```

For a custom component:

```jsx
<User name="Anurag" />
```

`name` becomes a prop.

For a DOM element:

```jsx
<input value={name} />
```

`value` is a DOM property/attribute handled by React.

---

# 📌 Part 2 — State

## 9. What is State in React?

State is data managed by a component that can change over time.

Example:

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

Here:

```text
count
```

is the current state.

```text
setCount
```

is the state updater.

---

## 10. Why do we need State?

State is used when changing data should cause the UI to update.

Examples:

* Counter value
* Login status
* Search input
* Shopping cart
* Modal visibility
* Selected category
* Loading state
* Form values

Example:

```jsx
const [isOpen, setIsOpen] = useState(false);
```

---

## 11. How do you create State?

Using the `useState` Hook:

```jsx
const [count, setCount] = useState(0);
```

The array contains:

```text
count     → current value
setCount  → updater function
```

---

## 12. What is the initial state?

The value passed to `useState()` is the initial state.

```jsx
const [count, setCount] = useState(0);
```

Initial state:

```text
0
```

Another example:

```jsx
const [user, setUser] = useState(null);
```

Initial state:

```text
null
```

---

## 13. Can State store objects?

Yes.

```jsx
const [user, setUser] = useState({
  name: "Anurag",
  age: 21
});
```

When updating an object, preserve the existing properties you want to keep.

```jsx
setUser(prevUser => ({
  ...prevUser,
  age: 22
}));
```

---

## 14. Can State store arrays?

Yes.

```jsx
const [products, setProducts] = useState([]);
```

Adding a product:

```jsx
setProducts(prevProducts => [
  ...prevProducts,
  newProduct
]);
```

The original array is not mutated.

---

# 📌 Part 3 — Props vs State

## 15. What is the difference between Props and State?

| Props                              | State                                                                 |
| ---------------------------------- | --------------------------------------------------------------------- |
| Passed into a component            | Managed by component                                                  |
| Read-only from child's perspective | Updated using state setter                                            |
| Controlled by parent/owner         | Owned by the component that manages it                                |
| Used to configure components       | Used for changing data                                                |
| Can be functions                   | Can contain any serializable/non-serializable JS value as appropriate |

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

## 16. Can Props cause a component to re-render?

Yes.

When a component receives new props, React may render it again.

Example:

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>
        {count}
      </button>

      <Child count={count} />
    </>
  );
}
```

When `count` changes, `Child` receives a new prop and can render again.

---

## 17. Can State cause a component to re-render?

Yes.

For example:

```jsx
const [count, setCount] = useState(0);

setCount(1);
```

React schedules an update, and the component renders again.

React then reconciles the new UI with the previous one and commits necessary changes.

---

# 📌 Part 4 — Updating State

## 18. How do you update State?

Use the updater function returned by `useState`.

```jsx
const [count, setCount] = useState(0);

setCount(10);
```

Do not directly assign:

```jsx
count = 10;
```

The setter tells React that the state needs to be updated.

---

## 19. Why shouldn't we modify State directly?

Incorrect:

```jsx
const [user, setUser] = useState({
  name: "Anurag"
});

user.name = "Rahul";
```

This mutates the existing object and does not correctly communicate the update to React.

Instead:

```jsx
setUser(prevUser => ({
  ...prevUser,
  name: "Rahul"
}));
```

This creates a new object.

---

## 20. How do you update an object in State?

Use the spread operator.

```jsx
const [user, setUser] = useState({
  name: "Anurag",
  age: 21
});

setUser(prevUser => ({
  ...prevUser,
  age: 22
}));
```

Result:

```text
{
  name: "Anurag",
  age: 22
}
```

---

## 21. How do you update an array in State?

Use non-mutating array operations.

### Add

```jsx
setItems(prevItems => [
  ...prevItems,
  newItem
]);
```

### Remove

```jsx
setItems(prevItems =>
  prevItems.filter(item => item.id !== id)
);
```

### Update

```jsx
setItems(prevItems =>
  prevItems.map(item =>
    item.id === id
      ? { ...item, completed: true }
      : item
  )
);
```

Avoid:

```jsx
items.push(newItem);
```

because that mutates the existing array.

---

# 📌 Part 5 — Functional State Updates

## 22. What is a functional state update?

A functional state update passes a function to the state setter.

```jsx
setCount(prevCount => prevCount + 1);
```

This is useful when the next state depends on the previous state.

---

## 23. Why use functional updates?

Consider:

```jsx
setCount(count + 1);
setCount(count + 1);
```

Both updates may calculate from the same captured `count` value.

Instead:

```jsx
setCount(prev => prev + 1);
setCount(prev => prev + 1);
```

Each update uses the latest pending state.

This is the preferred pattern when multiple updates depend on previous state.

---

## 24. What is the difference between these two?

### Direct update

```jsx
setCount(count + 1);
```

### Functional update

```jsx
setCount(prev => prev + 1);
```

Use the functional form when the new state depends on the previous state.

Example:

```jsx
setCount(prev => prev + 1);
```

---

# 📌 Part 6 — State Batching

## 25. What is State Batching?

Batching means React can group multiple state updates into a single render.

Example:

```jsx
function handleClick() {
  setFirstName("Anurag");
  setLastName("Kumar");
  setAge(22);
}
```

React can process these updates together rather than rendering separately for each setter call.

Modern React performs automatic batching in many asynchronous contexts as well.

---

## 26. Does every `setState` cause an immediate DOM update?

No.

Calling a state setter schedules an update. React can batch updates and process them together.

Example:

```jsx
setCount(prev => prev + 1);
console.log(count);
```

The `console.log` still sees the value from the current render.

It does not immediately change the JavaScript variable `count` inside that already-running render.

---

## 27. Why does State sometimes look "one step behind"?

Consider:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  function handleClick() {
    setCount(count + 1);

    console.log(count);
  }

  return (
    <button onClick={handleClick}>
      {count}
    </button>
  );
}
```

The log shows the `count` value from the current render.

State updates schedule a new render; they do not mutate the current render's local variables.

---

# 📌 Part 7 — State and Immutability

## 28. What is Immutability in React?

Immutability means we avoid modifying existing state objects and arrays directly.

Instead, we create new values.

Incorrect:

```jsx
user.name = "Rahul";
```

Correct:

```jsx
setUser(prev => ({
  ...prev,
  name: "Rahul"
}));
```

---

## 29. Why is Immutability important?

It helps React and developers reason about state changes more predictably.

Benefits include:

* Easier debugging
* Predictable state updates
* Easier change detection
* Better compatibility with memoization
* Avoiding accidental shared mutations

---

## 30. How do you remove an item from an array in State?

Use `filter()`.

```jsx
const removeItem = (id) => {
  setItems(prevItems =>
    prevItems.filter(item => item.id !== id)
  );
};
```

The original array is not mutated.

---

## 31. How do you update an item in an array?

Use `map()`.

```jsx
setItems(prevItems =>
  prevItems.map(item =>
    item.id === id
      ? { ...item, quantity: item.quantity + 1 }
      : item
  )
);
```

Only the matching item receives a new object.

---

# 📌 Part 8 — Derived State

## 32. What is Derived State?

Derived state is a value that can be calculated from existing props or state.

Example:

```jsx
const [products, setProducts] = useState([]);
const [search, setSearch] = useState("");

const filteredProducts = products.filter(product =>
  product.name
    .toLowerCase()
    .includes(search.toLowerCase())
);
```

`filteredProducts` is derived from:

```text
products
search
```

It usually does not need its own state.

---

## 33. Why shouldn't we store unnecessary derived state?

Suppose we have:

```jsx
const [products, setProducts] = useState([]);
const [filteredProducts, setFilteredProducts] = useState([]);
```

Now both states must stay synchronized.

This can create bugs.

Instead:

```jsx
const filteredProducts = products.filter(
  product => product.category === category
);
```

Calculate it from the source state.

---

## 34. When should derived data use `useMemo()`?

If a calculation is genuinely expensive and memoization provides a measurable benefit, `useMemo()` can cache the result between renders.

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

Do not automatically use `useMemo()` for every calculation.

---

# 📌 Part 9 — Lifting State

## 35. What is Lifting State Up?

Lifting state up means moving shared state to the closest common parent of the components that need it.

Example:

```text
             Parent
            /      \
       SearchBar   ProductList
```

Parent owns:

```jsx
const [search, setSearch] = useState("");
```

Then:

```jsx
<SearchBar
  search={search}
  setSearch={setSearch}
/>

<ProductList
  search={search}
/>
```

---

## 36. Why do we lift State up?

Because multiple components may need to access or modify the same data.

Example:

```text
SearchBar
    ↓
 search query
    ↓
ProductList
```

The parent becomes the **single source of truth**.

---

# 📌 Part 10 — State Ownership

## 37. What is "single source of truth"?

It means a particular piece of data should ideally have one authoritative owner.

For example:

```jsx
function App() {
  const [cart, setCart] = useState([]);

  return (
    <>
      <Navbar cart={cart} />
      <ProductList
        cart={cart}
        setCart={setCart}
      />
    </>
  );
}
```

Both components use the same cart state.

Instead of maintaining separate conflicting copies, the parent owns the state.

---

## 38. Where should State be stored?

State should generally live in the **closest component that needs to own/control it**.

If only one component needs it:

```text
Component
   ↓
Local State
```

If multiple siblings need it:

```text
Common Parent
   ↓
Shared State
```

If many distant parts of the application need it:

```text
Context / External Store
```

The choice depends on the application's requirements.

---

# 📌 Part 11 — Props and State Interview Traps

## 39. Can a child modify Parent State?

Not directly.

The parent can pass a callback.

```jsx
function Parent() {
  const [name, setName] = useState("");

  return (
    <Child
      name={name}
      setName={setName}
    />
  );
}
```

Child:

```jsx
function Child({ setName }) {
  return (
    <button onClick={() => setName("Anurag")}>
      Set Name
    </button>
  );
}
```

The parent still owns the state.

---

## 40. Can we pass State as Props?

Yes.

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return (
    <Child
      count={count}
      setCount={setCount}
    />
  );
}
```

Child receives:

```jsx
function Child({ count, setCount }) {
  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

---

## 41. Can we pass Props to another component as Props?

Yes.

```jsx
function Parent() {
  const user = {
    name: "Anurag"
  };

  return <Middle user={user} />;
}

function Middle({ user }) {
  return <Profile user={user} />;
}

function Profile({ user }) {
  return <h1>{user.name}</h1>;
}
```

This is one form of prop drilling.

---

## 42. Can we pass a component through Props?

Yes.

Example:

```jsx
function Layout({ header }) {
  return (
    <div>
      {header}
    </div>
  );
}
```

Usage:

```jsx
<Layout header={<Navbar />} />
```

This is a form of component composition.

---

# 📌 Part 12 — Props vs State: Interview Scenarios

## 43. A product name comes from an API. Should it be Props or State?

It depends on ownership.

If a parent fetches the product and passes it to a child:

```jsx
<ProductCard product={product} />
```

Then `product` is a **prop** inside `ProductCard`.

The parent may have the product in its own state.

So the same data can be:

```text
Parent:
product → State

Child:
product → Prop
```

---

## 44. Should API response data always be stored in State?

If the data affects the rendered UI and can change, it commonly belongs in state or a data-fetching/cache layer.

Example:

```jsx
const [products, setProducts] = useState([]);
```

Then:

```jsx
setProducts(data);
```

For larger applications, libraries such as TanStack Query can manage server state and caching instead of manually handling all of it with local state.

---

## 45. Should every value be stored in State?

No.

Don't put every variable into state.

For example:

```jsx
const firstName = "Anurag";
const lastName = "Kumar";

const fullName = `${firstName} ${lastName}`;
```

`fullName` does not need separate state because it can be calculated.

Use state when changing the value should participate in React's update process.

---

# 📌 Part 13 — Practical MERN Example

## 46. How would you manage Product State in an e-commerce application?

Example:

```jsx
function ProductPage() {
  const [product, setProduct] = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState(null);

  useEffect(() => {
    async function fetchProduct() {
      try {
        const response = await fetch("/api/products/123");
        const data = await response.json();

        setProduct(data);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    }

    fetchProduct();
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>Something went wrong.</p>;
  }

  return <ProductDetails product={product} />;
}
```

Here:

```text
product → State
loading → State
error → State
```

And:

```jsx
<ProductDetails product={product} />
```

passes `product` as a prop.

---

## 47. How would you manage a shopping cart?

A simple local implementation could use:

```jsx
const [cart, setCart] = useState([]);
```

Add item:

```jsx
const addToCart = (product) => {
  setCart(prevCart => [
    ...prevCart,
    product
  ]);
};
```

Remove item:

```jsx
const removeFromCart = (id) => {
  setCart(prevCart =>
    prevCart.filter(item => item._id !== id)
  );
};
```

For a larger application, cart state could be moved to Context or an external state-management solution depending on the requirements.

---

# 📌 Part 14 — Advanced Questions

## 48. What is state preservation in React?

React associates state with a component's position in the rendered tree.

If the same component remains at the same position, React can preserve its state between renders.

Example:

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
```

Switching between different component types can result in different state being created.

Understanding component identity and `key` is important for controlling when state is preserved or reset.

---

## 49. How can you reset a component's State?

One common technique is changing its `key`.

Example:

```jsx
<Form key={userId} />
```

When `userId` changes, React treats the component as a different identity and its local state can be reset.

This can be useful when displaying a fresh form for different users.

---

## 50. What happens if State is initialized from Props?

Example:

```jsx
function User({ name }) {
  const [username, setUsername] = useState(name);

  return (
    <input
      value={username}
      onChange={e =>
        setUsername(e.target.value)
      }
    />
  );
}
```

The initial value is taken from `name`.

However, later changes to `name` do **not automatically update** `username`.

This is because `useState(initialValue)` uses the initial value when the state is initialized.

If the value should always reflect the prop, you may not need local state at all.

---

## 51. Is copying Props into State a good idea?

Usually, no.

Avoid unnecessary duplication:

```jsx
const [name, setName] = useState(props.name);
```

if the component only needs to display the prop.

Prefer:

```jsx
<h1>{props.name}</h1>
```

Copy props into state only when you intentionally want an independent local value, such as an editable draft.

---

## 52. What is server state vs client state?

### Client State

State created and controlled by the UI.

Examples:

```text
Modal open/closed
Selected tab
Input value
Theme
Sidebar state
```

### Server State

Data that originates from a backend/server.

Examples:

```text
Products
Users
Orders
Complaints
Campaigns
```

Server state often needs:

* Fetching
* Caching
* Refetching
* Loading states
* Error handling
* Synchronization

Libraries such as TanStack Query can help manage server state.

---

# 🎯 Most Important Interview Questions

Before an interview, make sure you can explain:

```text
1. What are Props?
2. What is State?
3. Props vs State?
4. Can Props be modified?
5. How do you update State?
6. Why shouldn't State be mutated?
7. What is functional state update?
8. Why use previous state?
9. What is batching?
10. Why doesn't State update immediately?
11. What is immutability?
12. How do you update an object?
13. How do you update an array?
14. What is derived state?
15. What is lifting state up?
16. What is single source of truth?
17. How does child communicate with parent?
18. How do siblings share State?
19. Should every value be State?
20. What happens when State is initialized from Props?
21. What is server state?
22. Client state vs server state?
23. When should Context be used?
24. When should external state management be used?
25. How would you manage state in a MERN project?
```

---

# 🧠 Quick Revision

```text
                 React Data
                    │
          ┌─────────┴─────────┐
          ↓                   ↓
        Props                State
          │                   │
     Parent → Child       Component-owned
          │                   │
     Read-only input       Changes over time
          │                   │
          └─────────┬─────────┘
                    ↓
              UI Re-renders
                    ↓
              Reconciliation
                    ↓
             DOM Updates
```

---

# ⭐ Interview Formula

When asked **"Props vs State?"**, give this answer:

> **Props are read-only inputs passed into a component, usually from its parent, while state is data managed by a component that can change over time. Props are mainly used to configure and communicate with components, whereas state is used for dynamic data that should trigger UI updates.**

Then give an example:

```jsx
function ProductPage() {
  const [cart, setCart] = useState([]);

  return (
    <ProductCard
      cart={cart}
      setCart={setCart}
    />
  );
}
```

Here:

```text
cart
↓
State in ProductPage

cart
↓
Prop inside ProductCard
```

This distinction is **very important in React interviews**.
