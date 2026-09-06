# ⚛️ React Forms & Events — Interview Questions & Answers

A complete collection of **React Forms, Events, Controlled Components, Uncontrolled Components, Form Validation, and Event Handling** interview questions.

---

## 📚 Table of Contents

1. [What are Events in React?](#1-what-are-events-in-react)
2. [How are React Events Different from HTML Events?](#2-how-are-react-events-different-from-html-events)
3. [What is SyntheticEvent?](#3-what-is-syntheticevent)
4. [How do you Handle Click Events?](#4-how-do-you-handle-click-events)
5. [How do you Pass Arguments to an Event Handler?](#5-how-do-you-pass-arguments-to-an-event-handler)
6. [What is Event Object?](#6-what-is-event-object)
7. [What is `preventDefault()`?](#7-what-is-preventdefault)
8. [What is `stopPropagation()`?](#8-what-is-stoppropagation)
9. [What is Event Bubbling?](#9-what-is-event-bubbling)
10. [What is Event Capturing?](#10-what-is-event-capturing)
11. [What are Forms in React?](#11-what-are-forms-in-react)
12. [What is a Controlled Component?](#12-what-is-a-controlled-component)
13. [What is an Uncontrolled Component?](#13-what-is-an-uncontrolled-component)
14. [Controlled vs Uncontrolled Components](#14-controlled-vs-uncontrolled-components)
15. [How do you Handle Input Changes?](#15-how-do-you-handle-input-changes)
16. [How do you Handle Multiple Inputs?](#16-how-do-you-handle-multiple-inputs)
17. [How do you Handle Form Submission?](#17-how-do-you-handle-form-submission)
18. [How do you Reset a Form?](#18-how-do-you-reset-a-form)
19. [How do you Validate a Form?](#19-how-do-you-validate-a-form)
20. [How do you Handle Checkboxes?](#20-how-do-you-handle-checkboxes)
21. [How do you Handle Radio Buttons?](#21-how-do-you-handle-radio-buttons)
22. [How do you Handle Select Inputs?](#22-how-do-you-handle-select-inputs)
23. [How do you Handle File Inputs?](#23-how-do-you-handle-file-inputs)
24. [What is `FormData`?](#24-what-is-formdata)
25. [How do you Upload Images in React?](#25-how-do-you-upload-images-in-react)
26. [How do you Handle Loading During Submission?](#26-how-do-you-handle-loading-during-submission)
27. [How do you Prevent Multiple Submissions?](#27-how-do-you-prevent-multiple-submissions)
28. [How do you Handle API Errors in Forms?](#28-how-do-you-handle-api-errors-in-forms)
29. [How do you Build a Login Form?](#29-how-do-you-build-a-login-form)
30. [How do you Build a Registration Form?](#30-how-do-you-build-a-registration-form)
31. [Common Interview Questions](#31-common-interview-questions)
32. [MERN Project Examples](#32-mern-project-examples)
33. [Quick Revision](#33-quick-revision)

---

# 1. What are Events in React?

Events are actions that happen in the browser, such as:

* Click
* Input change
* Form submission
* Mouse movement
* Keyboard input
* Focus
* Blur

React allows us to handle these events using event handler props.

Example:

```jsx
function Button() {
  const handleClick = () => {
    console.log("Button clicked");
  };

  return (
    <button onClick={handleClick}>
      Click Me
    </button>
  );
}
```

---

# 2. How are React Events Different from HTML Events?

React uses camelCase event names.

HTML:

```html
<button onclick="handleClick()">
  Click
</button>
```

React:

```jsx
<button onClick={handleClick}>
  Click
</button>
```

Common examples:

```text
onclick       → onClick
onchange      → onChange
onsubmit      → onSubmit
onmouseover   → onMouseOver
onkeydown     → onKeyDown
```

React event handlers are passed as JavaScript functions.

---

# 3. What is SyntheticEvent?

React provides an event object with a consistent interface for handling events.

Example:

```jsx
function Input() {
  const handleChange = (event) => {
    console.log(event.target.value);
  };

  return <input onChange={handleChange} />;
}
```

The event object provides information such as:

```text
event.target
event.currentTarget
event.preventDefault()
event.stopPropagation()
```

Modern React uses the browser's event system while providing React's event API.

---

# 4. How do you Handle Click Events?

Use the `onClick` prop.

```jsx
function App() {
  const handleClick = () => {
    alert("Hello");
  };

  return (
    <button onClick={handleClick}>
      Click
    </button>
  );
}
```

Important:

Correct:

```jsx
onClick={handleClick}
```

Incorrect:

```jsx
onClick={handleClick()}
```

The second version calls the function during rendering instead of passing it as an event handler.

---

# 5. How do you Pass Arguments to an Event Handler?

Use an arrow function.

```jsx
function Product({ id }) {
  const handleDelete = (id) => {
    console.log(id);
  };

  return (
    <button onClick={() => handleDelete(id)}>
      Delete
    </button>
  );
}
```

React calls the arrow function when the button is clicked.

---

# 6. What is the Event Object?

React passes an event object to the event handler.

```jsx
function handleChange(event) {
  console.log(event);
}
```

For an input:

```jsx
function handleChange(event) {
  console.log(event.target.value);
}
```

Important properties:

```text
event.target
event.currentTarget
event.type
event.key
```

---

# 7. What is `preventDefault()`?

`preventDefault()` prevents the browser's default behavior.

For forms, the browser normally reloads/navigates when submitting.

React:

```jsx
function handleSubmit(event) {
  event.preventDefault();

  console.log("Form submitted");
}
```

Usage:

```jsx
<form onSubmit={handleSubmit}>
  ...
</form>
```

This allows React to handle the submission without the default browser navigation.

---

# 8. What is `stopPropagation()`?

`stopPropagation()` prevents an event from propagating further through the DOM event flow.

Example:

```jsx
function Child() {
  const handleClick = (event) => {
    event.stopPropagation();

    console.log("Child clicked");
  };

  return (
    <button onClick={handleClick}>
      Child
    </button>
  );
}
```

It is useful when a parent and child both have event handlers and you need to stop the child event from reaching the parent.

---

# 9. What is Event Bubbling?

Event bubbling means an event generally moves from the target element upward through its ancestors.

Example:

```jsx
<div onClick={() => console.log("Parent")}>
  <button onClick={() => console.log("Child")}>
    Click
  </button>
</div>
```

Clicking the button can produce:

```text
Child
  ↓
Parent
```

This is called bubbling.

---

# 10. What is Event Capturing?

Capturing is the opposite direction of event propagation.

Conceptually:

```text
Document
   ↓
Parent
   ↓
Child
```

A capture handler can be registered using:

```jsx
onClickCapture
```

Example:

```jsx
<div
  onClickCapture={() => {
    console.log("Capture");
  }}
>
  <button>Click</button>
</div>
```

---

# 11. What are Forms in React?

Forms allow users to enter and submit data.

Common form controls:

```text
input
textarea
select
checkbox
radio
button
```

Example:

```jsx
<form onSubmit={handleSubmit}>
  <input
    type="text"
    value={name}
    onChange={handleChange}
  />

  <button type="submit">
    Submit
  </button>
</form>
```

---

# 12. What is a Controlled Component?

A controlled input is an input whose value is controlled by React state.

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

The flow is:

```text
User types
    ↓
onChange
    ↓
setName()
    ↓
React state changes
    ↓
Input receives new value
```

---

# 13. What is an Uncontrolled Component?

An uncontrolled input stores its current value in the DOM rather than React state.

A ref can be used to access the value.

```jsx
function Form() {
  const inputRef = useRef(null);

  const handleSubmit = (e) => {
    e.preventDefault();

    console.log(inputRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={inputRef} />

      <button type="submit">
        Submit
      </button>
    </form>
  );
}
```

---

# 14. Controlled vs Uncontrolled Components

| Controlled                  | Uncontrolled                |
| --------------------------- | --------------------------- |
| Value stored in React state | Value stored in DOM         |
| Uses `value`                | Often uses `defaultValue`   |
| Uses `onChange`             | Often uses `ref`            |
| Easier real-time validation | Less React state management |
| More React-driven           | More DOM-driven             |

For many application forms, controlled components are convenient because React has direct access to the current values.

---

# 15. How do you Handle Input Changes?

Example:

```jsx
const [name, setName] = useState("");

const handleChange = (event) => {
  setName(event.target.value);
};
```

Then:

```jsx
<input
  value={name}
  onChange={handleChange}
/>
```

---

# 16. How do you Handle Multiple Inputs?

You can store multiple fields inside one object.

```jsx
const [form, setForm] = useState({
  name: "",
  email: "",
  password: ""
});
```

Generic handler:

```jsx
const handleChange = (event) => {
  const { name, value } = event.target;

  setForm(prev => ({
    ...prev,
    [name]: value
  }));
};
```

Inputs:

```jsx
<input
  name="name"
  value={form.name}
  onChange={handleChange}
/>

<input
  name="email"
  value={form.email}
  onChange={handleChange}
/>

<input
  name="password"
  type="password"
  value={form.password}
  onChange={handleChange}
/>
```

This is a very common interview pattern.

---

# 17. How do you Handle Form Submission?

Use `onSubmit`.

```jsx
function handleSubmit(event) {
  event.preventDefault();

  console.log(form);
}
```

Then:

```jsx
<form onSubmit={handleSubmit}>
  ...
  <button type="submit">
    Submit
  </button>
</form>
```

Using `onSubmit` on the form is generally better than attaching the main submission logic only to the button's `onClick`.

---

# 18. How do you Reset a Form?

For a controlled form:

```jsx
setForm({
  name: "",
  email: "",
  password: ""
});
```

Example:

```jsx
const initialForm = {
  name: "",
  email: "",
  password: ""
};

const [form, setForm] = useState(initialForm);

const handleReset = () => {
  setForm(initialForm);
};
```

Button:

```jsx
<button type="button" onClick={handleReset}>
  Reset
</button>
```

---

# 19. How do you Validate a Form?

You can validate fields before submitting.

Example:

```jsx
const validate = () => {
  const errors = {};

  if (!form.name.trim()) {
    errors.name = "Name is required";
  }

  if (!form.email.includes("@")) {
    errors.email = "Invalid email";
  }

  if (form.password.length < 6) {
    errors.password =
      "Password must be at least 6 characters";
  }

  return errors;
};
```

Then:

```jsx
const handleSubmit = (e) => {
  e.preventDefault();

  const validationErrors = validate();

  if (Object.keys(validationErrors).length > 0) {
    setErrors(validationErrors);
    return;
  }

  // submit form
};
```

Important:

> Client-side validation improves user experience, but server-side validation is still required for security and correctness.

---

# 20. How do you Handle Checkboxes?

For a single checkbox:

```jsx
const [accepted, setAccepted] = useState(false);
```

```jsx
<input
  type="checkbox"
  checked={accepted}
  onChange={(e) =>
    setAccepted(e.target.checked)
  }
/>
```

Use:

```text
checked
```

instead of:

```text
value
```

for the checkbox's boolean state.

---

# 21. How do you Handle Radio Buttons?

Example:

```jsx
const [role, setRole] = useState("user");
```

```jsx
<label>
  <input
    type="radio"
    name="role"
    value="user"
    checked={role === "user"}
    onChange={(e) => setRole(e.target.value)}
  />
  User
</label>

<label>
  <input
    type="radio"
    name="role"
    value="admin"
    checked={role === "admin"}
    onChange={(e) => setRole(e.target.value)}
  />
  Admin
</label>
```

The same `name` groups the radio buttons.

---

# 22. How do you Handle Select Inputs?

Example:

```jsx
const [category, setCategory] = useState("");
```

```jsx
<select
  value={category}
  onChange={(e) => setCategory(e.target.value)}
>
  <option value="">Select Category</option>
  <option value="books">Books</option>
  <option value="electronics">Electronics</option>
</select>
```

---

# 23. How do you Handle File Inputs?

File inputs are special because their value is controlled by the browser.

Example:

```jsx
const [file, setFile] = useState(null);

const handleFileChange = (e) => {
  setFile(e.target.files[0]);
};
```

```jsx
<input
  type="file"
  onChange={handleFileChange}
/>
```

You normally don't control the file input using a normal `value` state variable.

---

# 24. What is `FormData`?

`FormData` is a browser API used to construct key/value pairs for sending form data, especially when files are involved.

Example:

```jsx
const formData = new FormData();

formData.append("name", form.name);
formData.append("email", form.email);
formData.append("image", file);
```

Then:

```jsx
await axios.post(
  "/api/products",
  formData
);
```

The browser/HTTP client can send this as `multipart/form-data`.

---

# 25. How do you Upload Images in React?

Example:

```jsx
const handleSubmit = async (e) => {
  e.preventDefault();

  const formData = new FormData();

  formData.append("name", form.name);
  formData.append("image", file);

  await axios.post(
    "/api/products",
    formData
  );
};
```

Backend frameworks such as Express commonly use multipart middleware to process the uploaded file.

In a MERN project, the image may then be uploaded to a service such as Cloudinary.

---

# 26. How do you Handle Loading During Submission?

Use state:

```jsx
const [loading, setLoading] = useState(false);
```

Example:

```jsx
const handleSubmit = async (e) => {
  e.preventDefault();

  setLoading(true);

  try {
    await axios.post("/api/login", form);
  } finally {
    setLoading(false);
  }
};
```

Button:

```jsx
<button
  type="submit"
  disabled={loading}
>
  {loading ? "Submitting..." : "Submit"}
</button>
```

---

# 27. How do you Prevent Multiple Submissions?

Disable the submit button while the request is running.

```jsx
<button
  type="submit"
  disabled={loading}
>
  {loading ? "Loading..." : "Submit"}
</button>
```

You should also handle duplicate requests safely on the backend when necessary.

---

# 28. How do you Handle API Errors in Forms?

Store an error message in state.

```jsx
const [error, setError] = useState("");

const handleSubmit = async (e) => {
  e.preventDefault();

  setError("");

  try {
    await axios.post("/api/login", form);
  } catch (error) {
    setError(
      error.response?.data?.message ||
      "Something went wrong"
    );
  }
};
```

Display:

```jsx
{error && (
  <p>{error}</p>
)}
```

---

# 29. How do you Build a Login Form?

Example:

```jsx
function Login() {
  const [form, setForm] = useState({
    email: "",
    password: ""
  });

  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");

  const handleChange = (e) => {
    const { name, value } = e.target;

    setForm(prev => ({
      ...prev,
      [name]: value
    }));
  };

  const handleSubmit = async (e) => {
    e.preventDefault();

    setLoading(true);
    setError("");

    try {
      await axios.post(
        "/api/auth/login",
        form,
        {
          withCredentials: true
        }
      );
    } catch (error) {
      setError(
        error.response?.data?.message ||
        "Login failed"
      );
    } finally {
      setLoading(false);
    }
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        name="email"
        type="email"
        value={form.email}
        onChange={handleChange}
        placeholder="Email"
      />

      <input
        name="password"
        type="password"
        value={form.password}
        onChange={handleChange}
        placeholder="Password"
      />

      {error && <p>{error}</p>}

      <button
        type="submit"
        disabled={loading}
      >
        {loading ? "Logging in..." : "Login"}
      </button>
    </form>
  );
}
```

This demonstrates several important concepts:

```text
useState
controlled inputs
onChange
onSubmit
preventDefault
async/await
loading state
error handling
Axios
credentials
```

---

# 30. How do you Build a Registration Form?

A registration form usually contains:

```text
Name
Email
Password
Confirm Password
Role
Profile Image
```

Example state:

```jsx
const [form, setForm] = useState({
  name: "",
  email: "",
  password: "",
  confirmPassword: "",
  role: "user"
});
```

Before submitting:

```jsx
if (form.password !== form.confirmPassword) {
  setError("Passwords do not match");
  return;
}
```

Then send the data to the backend.

---

# 31. What is the difference between `onChange` and `onInput`?

Both can be used to respond to changes in form controls, but React's `onChange` is the standard choice for controlled form inputs.

Example:

```jsx
<input
  value={name}
  onChange={e => setName(e.target.value)}
/>
```

For normal React forms, `onChange` is what you should generally use.

---

# 32. What is the difference between `value` and `defaultValue`?

### `value`

Used for a controlled input:

```jsx
<input
  value={name}
  onChange={handleChange}
/>
```

React controls the current value.

### `defaultValue`

Used to provide an initial value for an uncontrolled input:

```jsx
<input defaultValue="Anurag" />
```

After initialization, the DOM manages the current value.

---

# 33. What is a controlled checkbox?

Use `checked`:

```jsx
<input
  type="checkbox"
  checked={isSelected}
  onChange={e =>
    setIsSelected(e.target.checked)
  }
/>
```

Not:

```jsx
<input
  type="checkbox"
  value={isSelected}
/>
```

`value` represents the submitted value, while `checked` represents whether the checkbox is selected.

---

# 34. What happens if you provide `value` without `onChange`?

Example:

```jsx
<input value={name} />
```

React treats it as a controlled input, but there is no handler to update its value.

This can make the input effectively read-only and may produce a warning.

If you want a controlled editable input:

```jsx
<input
  value={name}
  onChange={e => setName(e.target.value)}
/>
```

---

# 35. What is a controlled/uncontrolled warning?

React warns when an input changes between controlled and uncontrolled states.

For example, this can happen when an input initially receives:

```jsx
value={undefined}
```

and later receives:

```jsx
value="Anurag"
```

A common solution is to initialize string fields with:

```jsx
const [name, setName] = useState("");
```

instead of `undefined`.

---

# 36. How do you validate email in React?

Simple validation:

```jsx
const emailRegex =
  /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

if (!emailRegex.test(form.email)) {
  setError("Invalid email");
}
```

However, client-side regex validation should not replace backend validation.

---

# 37. How do you show field-specific errors?

Store errors by field.

```jsx
const [errors, setErrors] = useState({});
```

Example:

```jsx
setErrors({
  email: "Invalid email",
  password: "Password is too short"
});
```

Then:

```jsx
{errors.email && (
  <p>{errors.email}</p>
)}
```

This provides better UX than showing one generic error.

---

# 38. How do you handle password confirmation?

```jsx
if (
  form.password !==
  form.confirmPassword
) {
  setErrors({
    confirmPassword:
      "Passwords do not match"
  });

  return;
}
```

The frontend can provide immediate feedback.

The backend should still validate the actual password requirements.

---

# 39. How do you handle a textarea?

`textarea` can be controlled just like an input.

```jsx
const [description, setDescription] = useState("");

<textarea
  value={description}
  onChange={e =>
    setDescription(e.target.value)
  }
/>
```

---

# 40. How do you handle a dynamic list of form fields?

Suppose users can add multiple phone numbers.

```jsx
const [phones, setPhones] = useState([""]);
```

Add:

```jsx
setPhones(prev => [
  ...prev,
  ""
]);
```

Update:

```jsx
setPhones(prev =>
  prev.map((phone, index) =>
    index === targetIndex
      ? newValue
      : phone
  )
);
```

Remove:

```jsx
setPhones(prev =>
  prev.filter((_, index) =>
    index !== targetIndex
  )
);
```

---

# 41. How do you prevent form submission when validation fails?

```jsx
const handleSubmit = (e) => {
  e.preventDefault();

  const errors = validate();

  if (Object.keys(errors).length) {
    setErrors(errors);
    return;
  }

  submitForm();
};
```

The `return` prevents the API call from executing.

---

# 42. Why use `type="submit"` on a button?

Inside a form:

```jsx
<button type="submit">
  Login
</button>
```

clicking the button triggers the form's:

```jsx
onSubmit
```

handler.

This is preferable to putting all form submission logic only inside `onClick`.

---

# 43. Why should you use `<label>` with inputs?

Labels improve accessibility and usability.

Example:

```jsx
<label htmlFor="email">
  Email
</label>

<input
  id="email"
  type="email"
/>
```

Clicking the label can focus the associated input.

---

# 44. What is event delegation?

Event delegation means handling events at a parent level instead of attaching separate handlers to every child.

Example:

```jsx
<ul onClick={handleClick}>
  <li data-id="1">Book</li>
  <li data-id="2">Pen</li>
  <li data-id="3">Bag</li>
</ul>
```

The parent can inspect:

```jsx
event.target.dataset.id
```

This can be useful for large dynamic lists.

React already uses a delegated event system internally for many events, so developers generally interact with the React event API rather than manually implementing delegation everywhere.

---

# 45. What is the difference between `event.target` and `event.currentTarget`?

This is a common interview question.

### `event.target`

The element where the event originated.

### `event.currentTarget`

The element whose event handler is currently handling the event.

Example:

```jsx
<div onClick={handleClick}>
  <button>Click</button>
</div>
```

If the button is clicked:

```text
target        → button
currentTarget → div
```

---

# 46. How do you handle keyboard events?

React provides:

```jsx
onKeyDown
onKeyUp
```

Example:

```jsx
<input
  onKeyDown={(e) => {
    if (e.key === "Enter") {
      console.log("Enter pressed");
    }
  }}
/>
```

This is useful for:

* Search
* Keyboard shortcuts
* Form submission
* Accessibility

---

# 47. How do you submit a form when Enter is pressed?

If the input is inside a proper `<form>` and the submit button is:

```jsx
<button type="submit">
  Search
</button>
```

the browser's normal form behavior can submit when Enter is pressed in appropriate controls.

This is generally preferable to manually listening for Enter everywhere.

---

# 48. How do you handle forms with React and Axios?

Example:

```jsx
const handleSubmit = async (e) => {
  e.preventDefault();

  try {
    const response = await axios.post(
      "/api/users",
      form
    );

    console.log(response.data);
  } catch (error) {
    console.error(error);
  }
};
```

Flow:

```text
Form
 ↓
onSubmit
 ↓
preventDefault()
 ↓
Validate
 ↓
Axios request
 ↓
Express API
 ↓
MongoDB
 ↓
Response
 ↓
Update React state
```

---

# 49. How do you handle a form with Cloudinary image upload?

Typical MERN flow:

```text
React Form
   ↓
Select Image
   ↓
FormData
   ↓
Express API
   ↓
Upload Middleware
   ↓
Cloudinary
   ↓
Cloudinary URL
   ↓
MongoDB
```

React example:

```jsx
const data = new FormData();

data.append("name", form.name);
data.append("image", file);

await axios.post(
  "/api/campaigns",
  data
);
```

This pattern is useful for profile images, campaign images, products, and complaint attachments.

---

# 50. What are common React form mistakes?

### Mistake 1 — Calling the handler immediately

Wrong:

```jsx
onClick={handleSubmit()}
```

Correct:

```jsx
onClick={handleSubmit}
```

---

### Mistake 2 — Forgetting `preventDefault()`

```jsx
const handleSubmit = (e) => {
  e.preventDefault();
};
```

---

### Mistake 3 — Mutating form state

Wrong:

```jsx
form.name = "Anurag";
```

Correct:

```jsx
setForm(prev => ({
  ...prev,
  name: "Anurag"
}));
```

---

### Mistake 4 — Using `value` for checkbox state

Wrong:

```jsx
checked={false}
```

without managing it correctly.

Correct:

```jsx
checked={accepted}
onChange={e =>
  setAccepted(e.target.checked)
}
```

---

### Mistake 5 — No backend validation

Frontend validation is not enough.

Always validate important data on the server.

---

# 💼 MERN Example: NGO Campaign Form

Suppose your NGO platform has a campaign creation form:

```jsx
const [form, setForm] = useState({
  title: "",
  description: "",
  targetAmount: ""
});

const [image, setImage] = useState(null);

const handleChange = (e) => {
  const { name, value } = e.target;

  setForm(prev => ({
    ...prev,
    [name]: value
  }));
};

const handleSubmit = async (e) => {
  e.preventDefault();

  const data = new FormData();

  data.append("title", form.title);
  data.append("description", form.description);
  data.append(
    "targetAmount",
    form.targetAmount
  );

  if (image) {
    data.append("image", image);
  }

  await axios.post(
    "/api/campaigns",
    data
  );
};
```

This demonstrates:

```text
Controlled form
       ↓
State management
       ↓
File input
       ↓
FormData
       ↓
Axios
       ↓
Express
       ↓
Cloudinary + MongoDB
```

---

# 💼 MERN Example: Civic Complaint Form

A complaint form might contain:

```text
Title
Description
Category
Priority
Location
Image
```

React state:

```jsx
const [form, setForm] = useState({
  title: "",
  description: "",
  category: "",
  priority: ""
});
```

On submission:

```text
React
 ↓
Validate
 ↓
FormData
 ↓
Express API
 ↓
AI classification
 ↓
MongoDB
 ↓
Socket.IO status update
 ↓
React UI
```

This is a strong real-world example to explain during a MERN interview.

---

# 🎯 Top 20 Form & Event Interview Questions

Make sure you can answer these without looking at notes:

1. What are events in React?
2. How are React events different from HTML events?
3. What is SyntheticEvent?
4. What is `event.target`?
5. What is `event.currentTarget`?
6. What is `preventDefault()`?
7. What is `stopPropagation()`?
8. What is event bubbling?
9. What is event capturing?
10. What is a controlled component?
11. What is an uncontrolled component?
12. Controlled vs uncontrolled components?
13. How do you handle multiple inputs?
14. How do you handle checkbox and radio inputs?
15. How do you handle file uploads?
16. What is `FormData`?
17. How do you validate a form?
18. How do you prevent duplicate submissions?
19. How do you handle API errors?
20. Explain a form you implemented in your MERN project.

---

# ⚡ Quick Revision

| Concept               | Purpose                       |
| --------------------- | ----------------------------- |
| `onClick`             | Handle click                  |
| `onChange`            | Handle form value changes     |
| `onSubmit`            | Handle form submission        |
| `onKeyDown`           | Handle keyboard input         |
| `preventDefault()`    | Stop browser default behavior |
| `stopPropagation()`   | Stop event propagation        |
| `event.target`        | Event origin element          |
| `event.currentTarget` | Element handling the event    |
| Controlled input      | Value managed by React        |
| Uncontrolled input    | Value managed by DOM          |
| `FormData`            | Build form/multipart data     |
| `checked`             | Checkbox/radio state          |
| `value`               | Input/select value            |
| `defaultValue`        | Initial uncontrolled value    |
| `useRef`              | Access uncontrolled input/DOM |
| Validation            | Check input before submission |

---

# 🧠 Interview Formula

For a React form, remember:

```text
User Input
    ↓
onChange
    ↓
Update State
    ↓
Validation
    ↓
onSubmit
    ↓
preventDefault()
    ↓
API Request
    ↓
Loading / Error Handling
    ↓
Backend Validation
    ↓
Database
    ↓
Update UI
```

### Most Important Concepts

> **Controlled components + `onChange` + `onSubmit` + `preventDefault()` + validation + API error handling** are the core React form concepts you should know for a MERN interview.
