# ⚛️ JSX – Interview Questions & Answers

> React JSX interview preparation — from fundamentals to commonly asked interview concepts.

---

## 1. What is JSX?

JSX stands for **JavaScript XML**.

It is a syntax extension that allows us to write HTML-like markup inside JavaScript code.

Example:

```jsx
function App() {
  return <h1>Hello React</h1>;
}
```

JSX makes React UI code easier to read and write.

---

## 2. Is JSX HTML?

No.

JSX **looks similar to HTML**, but it is not HTML.

For example:

```jsx
<h1 className="title">Hello</h1>
```

Here, `className` is used instead of HTML's `class`.

JSX follows JavaScript and React rules rather than being plain HTML.

---

## 3. Is JSX mandatory in React?

No.

JSX is optional.

React elements can also be created using JavaScript APIs.

```jsx
const element = React.createElement(
  "h1",
  null,
  "Hello"
);
```

However, JSX is much more readable for complex UI.

---

## 4. Why do we use JSX?

JSX provides a convenient way to describe UI directly inside JavaScript.

### Advantages

* Easy to read
* Easy to write
* Supports JavaScript expressions
* Makes component structure clear
* Improves maintainability
* Makes UI and component logic easier to understand together

Example:

```jsx
function User({ name, age }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>Age: {age}</p>
    </div>
  );
}
```

---

## 5. How does JSX work?

JSX is transformed by the React build tooling into JavaScript that React can use.

For example:

```jsx
const element = <h1>Hello</h1>;
```

With the modern JSX transform, this is compiled using JSX runtime functions.

Conceptually, the result represents a React element.

Older React setups commonly transformed JSX into:

```javascript
React.createElement("h1", null, "Hello");
```

### Interview Answer

> JSX is not directly understood by the JavaScript engine. The build toolchain transforms JSX syntax into JavaScript that React can use to create elements.

---

## 6. What is the JSX transformation?

The JSX transformation converts JSX syntax into JavaScript.

Example:

```jsx
const element = <h1>Hello</h1>;
```

Conceptually:

```javascript
const element = React.createElement(
  "h1",
  null,
  "Hello"
);
```

Modern React projects can use the automatic JSX runtime, so manually importing `React` only for JSX is generally unnecessary.

---

## 7. What is the difference between JSX and `React.createElement()`?

### JSX

```jsx
const element = (
  <div>
    <h1>Hello</h1>
  </div>
);
```

### `React.createElement()`

```javascript
const element = React.createElement(
  "div",
  null,
  React.createElement(
    "h1",
    null,
    "Hello"
  )
);
```

JSX is much easier to read.

The JSX version is primarily **syntactic convenience** for describing React elements.

---

## 8. Can we use JavaScript expressions inside JSX?

Yes.

JavaScript expressions can be written inside `{}`.

Example:

```jsx
function App() {
  const name = "Anurag";
  const age = 21;

  return (
    <div>
      <h1>Hello {name}</h1>
      <p>Age: {age}</p>
    </div>
  );
}
```

---

## 9. What can we put inside `{}` in JSX?

We can put JavaScript **expressions** inside `{}`.

Examples:

### Variable

```jsx
<h1>{name}</h1>
```

### Arithmetic

```jsx
<p>{10 + 20}</p>
```

### Function call

```jsx
<p>{getName()}</p>
```

### Ternary operator

```jsx
<p>{age >= 18 ? "Adult" : "Minor"}</p>
```

### Array methods

```jsx
{users.map(user => (
  <p key={user.id}>{user.name}</p>
))}
```

---

## 10. Can we use an `if` statement directly inside JSX?

No.

This is invalid:

```jsx
return (
  <div>
    {if (isLoggedIn) {
      <Dashboard />
    }}
  </div>
);
```

Instead, use a variable, an early return, or a conditional expression.

### Ternary

```jsx
return (
  <div>
    {isLoggedIn ? <Dashboard /> : <Login />}
  </div>
);
```

### `if` before return

```jsx
function App({ isLoggedIn }) {
  if (isLoggedIn) {
    return <Dashboard />;
  }

  return <Login />;
}
```

---

## 11. What is the difference between an expression and a statement?

An **expression produces a value**.

Examples:

```javascript
10 + 20
```

```javascript
name
```

```javascript
age > 18 ? "Adult" : "Minor"
```

A **statement performs an action**.

Examples:

```javascript
if (age > 18) {
  console.log("Adult");
}
```

```javascript
for (let i = 0; i < 10; i++) {
}
```

JSX `{}` accepts expressions, not arbitrary statements.

---

## 12. Why do we use `className` instead of `class`?

`class` is a JavaScript keyword.

React uses:

```jsx
className
```

instead of:

```jsx
class
```

Example:

```jsx
<div className="container">
  Hello
</div>
```

This becomes the HTML `class` attribute in the browser.

---

## 13. What is `htmlFor` in JSX?

In JSX, the `<label>` attribute is:

```jsx
htmlFor
```

instead of HTML's:

```html
for
```

Example:

```jsx
<label htmlFor="email">
  Email
</label>

<input id="email" type="email" />
```

---

## 14. Why do JSX attributes use camelCase?

Many DOM properties and event handlers are written using JavaScript naming conventions.

Examples:

```jsx
className
tabIndex
onClick
onChange
onMouseEnter
```

Instead of HTML-style names such as:

```text
class
onclick
onchange
```

---

## 15. How do you add CSS classes in JSX?

Use `className`.

```jsx
function App() {
  return (
    <div className="container">
      <h1 className="title">Hello</h1>
    </div>
  );
}
```

With a dynamic class:

```jsx
<div className={isActive ? "active" : "inactive"}>
  Menu
</div>
```

---

## 16. How do you add inline styles in JSX?

Inline styles are passed as a JavaScript object.

```jsx
function App() {
  return (
    <h1
      style={{
        color: "red",
        fontSize: "24px"
      }}
    >
      Hello
    </h1>
  );
}
```

Notice:

```jsx
fontSize
```

instead of:

```css
font-size
```

because the style object uses JavaScript property naming.

---

## 17. How do you use variables in JSX?

Use `{}`.

```jsx
function App() {
  const username = "Anurag";

  return <h1>Welcome {username}</h1>;
}
```

Output:

```text
Welcome Anurag
```

---

## 18. How do you render a list using JSX?

Use JavaScript's `map()` method.

```jsx
function Users() {
  const users = [
    { id: 1, name: "Anurag" },
    { id: 2, name: "Rahul" },
    { id: 3, name: "Aman" }
  ];

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

The `key` should be stable and unique among the siblings.

---

## 19. Why do we need a `key` when rendering lists?

Keys help React identify which list item corresponds to which element between renders.

Example:

```jsx
{users.map(user => (
  <User
    key={user.id}
    user={user}
  />
))}
```

Stable keys help React correctly handle:

* Insertions
* Deletions
* Reordering
* Updates

---

## 20. Can we use index as a key?

Yes, technically.

```jsx
users.map((user, index) => (
  <User key={index} user={user} />
));
```

But it is generally not recommended when the list can change order or have items inserted/removed.

Prefer:

```jsx
<User key={user.id} />
```

when a stable ID exists.

Index keys can be reasonable for static lists whose order never changes.

---

## 21. Can JSX return multiple elements?

Yes.

You can return multiple elements by wrapping them in a parent element.

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>Welcome</p>
  </div>
);
```

However, adding an unnecessary DOM element is sometimes undesirable.

In that case, use a Fragment.

---

## 22. What is a React Fragment?

A Fragment allows multiple elements to be grouped without adding an extra DOM element.

### Short syntax

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>Welcome</p>
  </>
);
```

### Explicit syntax

```jsx
return (
  <React.Fragment>
    <h1>Hello</h1>
    <p>Welcome</p>
  </React.Fragment>
);
```

---

## 23. Why use Fragment instead of `<div>`?

Consider:

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>Welcome</p>
  </div>
);
```

This adds an extra `<div>` to the DOM.

Instead:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>Welcome</p>
  </>
);
```

No additional wrapper element is created.

---

## 24. Can Fragment have a key?

Yes.

When rendering a list, use the explicit Fragment syntax because the shorthand `<>...</>` cannot receive a `key`.

```jsx
items.map(item => (
  <React.Fragment key={item.id}>
    <h2>{item.name}</h2>
    <p>{item.description}</p>
  </React.Fragment>
))
```

---

## 25. How do you add comments in JSX?

Use JavaScript-style comments inside braces.

```jsx
function App() {
  return (
    <div>
      {/* This is a JSX comment */}
      <h1>Hello</h1>
    </div>
  );
}
```

This is not correct:

```jsx
<!-- comment -->
```

That is an HTML comment, not JSX syntax.

---

## 26. What is conditional rendering in JSX?

Conditional rendering means displaying different UI based on a condition.

### Ternary

```jsx
return (
  <div>
    {isLoggedIn ? <Dashboard /> : <Login />}
  </div>
);
```

### Logical AND

```jsx
{isAdmin && <AdminPanel />}
```

### Early return

```jsx
if (!user) {
  return <Login />;
}

return <Dashboard />;
```

---

## 27. What happens when JSX evaluates to `null`?

React renders nothing for:

```jsx
return null;
```

Example:

```jsx
function AdminPanel({ isAdmin }) {
  if (!isAdmin) {
    return null;
  }

  return <div>Admin Panel</div>;
}
```

This is useful when a component should conditionally render nothing.

---

## 28. What happens when we render `false`, `true`, or `null`?

React does not render these values as visible text.

For example:

```jsx
<div>
  {false}
  {true}
  {null}
</div>
```

These do not create visible text nodes.

This is why the following works:

```jsx
{isLoggedIn && <Dashboard />}
```

When `isLoggedIn` is `false`, React renders nothing for that expression.

---

## 29. What happens when we render a number in JSX?

Numbers can be rendered.

```jsx
const age = 21;

return <p>{age}</p>;
```

Output:

```text
21
```

---

## 30. What happens when we render an object directly in JSX?

Generally, you cannot render a plain object directly as a React child.

Incorrect:

```jsx
const user = {
  name: "Anurag",
  age: 21
};

return <div>{user}</div>;
```

Instead, access its properties:

```jsx
return (
  <div>
    <p>{user.name}</p>
    <p>{user.age}</p>
  </div>
);
```

Or convert it to a string when appropriate:

```jsx
<pre>{JSON.stringify(user, null, 2)}</pre>
```

---

## 31. Can JSX contain nested components?

Yes.

```jsx
function App() {
  return (
    <div>
      <Navbar />
      <Main />
      <Footer />
    </div>
  );
}
```

Here:

```text
App
 ├── Navbar
 ├── Main
 └── Footer
```

This is one of the main benefits of component-based architecture.

---

## 32. What is a JSX attribute?

A JSX attribute provides information to an element or component.

Example:

```jsx
<img
  src="/profile.png"
  alt="Profile"
/>
```

Here:

```text
src
alt
```

are JSX attributes.

For components, attributes become props:

```jsx
<User name="Anurag" />
```

Here `name` is passed as a prop.

---

## 33. How do you pass a JavaScript value as a JSX attribute?

Use `{}`.

```jsx
const age = 21;

<User age={age} />
```

For strings, you can use:

```jsx
<User name="Anurag" />
```

Both are valid.

---

## 34. What is the difference between these two?

```jsx
<User age="21" />
```

and:

```jsx
<User age={21} />
```

The first passes a **string**:

```text
"21"
```

The second passes a **number**:

```text
21
```

Example:

```jsx
function User({ age }) {
  console.log(typeof age);
}
```

First:

```text
string
```

Second:

```text
number
```

---

## 35. What is spread syntax in JSX?

Spread syntax allows us to pass multiple object properties as props.

```jsx
const user = {
  name: "Anurag",
  age: 21
};

<User {...user} />
```

This is similar to:

```jsx
<User
  name={user.name}
  age={user.age}
/>
```

---

## 36. Can we use functions inside JSX?

Yes.

You can call functions:

```jsx
<p>{getUsername()}</p>
```

You can also pass functions as event handlers:

```jsx
<button onClick={handleClick}>
  Click
</button>
```

---

## 37. What is the difference between `onClick={handleClick}` and `onClick={handleClick()}`?

This is a very common interview question.

### Correct

```jsx
<button onClick={handleClick}>
  Click
</button>
```

React receives the function and calls it when the event occurs.

### Usually incorrect

```jsx
<button onClick={handleClick()}>
  Click
</button>
```

This calls the function during rendering instead of passing the function as the event handler.

If arguments are required:

```jsx
<button onClick={() => handleClick(id)}>
  Click
</button>
```

---

## 38. Can JSX use `for` loops?

Not directly inside `{}` because a `for` loop is a statement.

Instead, use `map()` for rendering collections.

```jsx
{users.map(user => (
  <p key={user.id}>
    {user.name}
  </p>
))}
```

Or build the data before returning JSX.

---

## 39. What is JSX nesting?

JSX elements can be nested.

```jsx
<div>
  <h1>Hello</h1>

  <section>
    <p>Welcome to React</p>
  </section>
</div>
```

The nesting represents the UI structure.

---

## 40. What are self-closing JSX tags?

Elements without children can be self-closed.

Instead of:

```jsx
<img src="image.png"></img>
```

write:

```jsx
<img src="image.png" />
```

Similarly:

```jsx
<User />
```

instead of:

```jsx
<User></User>
```

---

## 41. Why must JSX elements be properly closed?

JSX follows XML-like syntax rules.

Correct:

```jsx
<img src="image.png" />
```

Incorrect:

```jsx
<img src="image.png">
```

For non-void elements:

```jsx
<div></div>
```

or:

```jsx
<div />
```

---

## 42. Why must JSX return a single parent?

A component's returned JSX must represent one React element tree.

Incorrect:

```jsx
return (
  <h1>Hello</h1>
  <p>Welcome</p>
);
```

Correct:

```jsx
return (
  <div>
    <h1>Hello</h1>
    <p>Welcome</p>
  </div>
);
```

Or use a Fragment:

```jsx
return (
  <>
    <h1>Hello</h1>
    <p>Welcome</p>
  </>
);
```

---

## 43. Can JSX use ternary operators?

Yes.

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

Ternary operators are useful for choosing between two UI states.

---

## 44. What is the difference between `&&` and ternary in JSX?

### `&&`

Useful when you want to render something only when a condition is true.

```jsx
{isAdmin && <AdminPanel />}
```

### Ternary

Useful when you have two possible UI branches.

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
```

---

## 45. What is the `children` prop?

Content placed between a component's opening and closing tags is received through the `children` prop.

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

The content between `<Card>` and `</Card>` becomes:

```jsx
children
```

---

## 46. How is JSX used in reusable components?

JSX makes it easy to create reusable UI components.

Example:

```jsx
function Button({ children }) {
  return (
    <button className="btn">
      {children}
    </button>
  );
}
```

Usage:

```jsx
<Button>
  Login
</Button>

<Button>
  Register
</Button>
```

The same component can render different content.

---

## 47. What is dynamic JSX?

Dynamic JSX means UI changes based on JavaScript data.

Example:

```jsx
function Product({ product }) {
  return (
    <div>
      <h2>{product.name}</h2>
      <p>₹{product.price}</p>

      {product.inStock ? (
        <button>Buy Now</button>
      ) : (
        <p>Out of Stock</p>
      )}
    </div>
  );
}
```

This is common in real-world React applications.

---

## 48. Can we use async/await directly inside JSX?

No.

You should not write:

```jsx
return <div>{await getData()}</div>;
```

in a normal client component.

Instead, fetch data through an appropriate data-fetching mechanism and store/use the result.

For example:

```jsx
useEffect(() => {
  async function fetchProducts() {
    const response = await fetch("/api/products");
    const data = await response.json();
    setProducts(data);
  }

  fetchProducts();
}, []);
```

Server components in frameworks such as Next.js have different capabilities, so this distinction matters in interviews.

---

## 49. Can JSX access component state?

Yes.

Example:

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

Here `count` is used inside JSX.

When the state changes, React updates the UI accordingly.

---

## 50. What is the most important thing to remember about JSX?

Remember:

```text
JSX
 ↓
HTML-like syntax
 ↓
Written inside JavaScript
 ↓
Supports JavaScript expressions using {}
 ↓
Transformed by tooling
 ↓
Used to describe React UI
```

### Quick Interview Answer

> JSX is a JavaScript syntax extension used by React to describe UI using HTML-like syntax. It allows JavaScript expressions inside `{}` and is transformed by the build toolchain into JavaScript that React can use to create and update the UI.

---

# 🎯 JSX Interview Quick Revision

### Must Know

```text
1. What is JSX?
2. Is JSX HTML?
3. Is JSX mandatory?
4. How does JSX work?
5. JSX vs createElement()
6. Expressions inside JSX
7. className vs class
8. htmlFor vs for
9. Inline styles
10. Conditional rendering
11. Rendering lists
12. Keys
13. Fragments
14. JSX comments
15. Props in JSX
16. Spread props
17. children
18. Event handlers
19. Ternary vs &&
20. JSX and JavaScript statements
```

---

# 💡 MERN Interview Example

Suppose your React application displays products received from your Express API.

```jsx
function ProductList({ products }) {
  return (
    <div className="grid">
      {products.map(product => (
        <div key={product._id}>
          <img
            src={product.image}
            alt={product.name}
          />

          <h2>{product.name}</h2>

          <p>₹{product.price}</p>

          {product.stock > 0 ? (
            <button>Add to Cart</button>
          ) : (
            <p>Out of Stock</p>
          )}
        </div>
      ))}
    </div>
  );
}
```

This single example demonstrates several important JSX concepts:

* JavaScript expressions
* Props
* `map()`
* Keys
* Conditional rendering
* Dynamic attributes
* Components
* Event handlers
* API-driven UI

These are exactly the types of concepts you should be able to explain during a **MERN Stack interview**.
