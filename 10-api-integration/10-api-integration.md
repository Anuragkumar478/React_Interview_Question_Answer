# ⚛️ React API Integration — Interview Questions & Answers

API integration is one of the most important topics for **React and MERN Stack interviews**.

A React frontend usually communicates with a backend through HTTP APIs.

Typical MERN flow:

```text
React
  ↓
Axios / Fetch
  ↓
Express.js API
  ↓
Controller
  ↓
MongoDB
  ↓
JSON Response
  ↓
React State
  ↓
UI
```

This file covers:

* REST APIs
* HTTP methods
* `fetch`
* Axios
* GET/POST/PUT/PATCH/DELETE
* `async/await`
* Loading states
* Error handling
* Authentication
* Cookies
* Axios interceptors
* CRUD
* Pagination
* Search
* File uploads
* Request cancellation
* Optimistic updates
* MERN API architecture

---

## 📚 Table of Contents

1. [What is an API?](#1-what-is-an-api)
2. [What is API Integration?](#2-what-is-api-integration)
3. [How Does React Communicate with a Backend?](#3-how-does-react-communicate-with-a-backend)
4. [What is REST API?](#4-what-is-rest-api)
5. [HTTP Methods](#5-http-methods)
6. [GET Request](#6-get-request)
7. [POST Request](#7-post-request)
8. [PUT vs PATCH](#8-put-vs-patch)
9. [DELETE Request](#9-delete-request)
10. [What is JSON?](#10-what-is-json)
11. [Fetch API](#11-fetch-api)
12. [Axios](#12-axios)
13. [Fetch vs Axios](#13-fetch-vs-axios)
14. [async/await](#14-asyncawait)
15. [API Call in useEffect](#15-api-call-in-useeffect)
16. [Loading State](#16-loading-state)
17. [Error Handling](#17-error-handling)
18. [Complete GET Example](#18-complete-get-example)
19. [POST API Example](#19-post-api-example)
20. [CRUD Operations](#20-crud-operations)
21. [What is Axios Instance?](#21-what-is-axios-instance)
22. [What are Axios Interceptors?](#22-what-are-axios-interceptors)
23. [Authentication with APIs](#23-authentication-with-apis)
24. [Cookies and API Requests](#24-cookies-and-api-requests)
25. [Authorization Headers](#25-authorization-headers)
26. [Handling 401 Errors](#26-handling-401-errors)
27. [Environment Variables](#27-environment-variables)
28. [CORS](#28-cors)
29. [Request Timeout](#29-request-timeout)
30. [Request Cancellation](#30-request-cancellation)
31. [Race Conditions](#31-race-conditions)
32. [Search API](#32-search-api)
33. [Debounced Search](#33-debounced-search)
34. [Pagination](#34-pagination)
35. [Filtering](#35-filtering)
36. [Sorting](#36-sorting)
37. [File Upload](#37-file-upload)
38. [FormData](#38-formdata)
39. [API Response Structure](#39-api-response-structure)
40. [Optimistic Updates](#40-optimistic-updates)
41. [Retrying API Requests](#41-retrying-api-requests)
42. [Avoiding Duplicate API Requests](#42-avoiding-duplicate-api-requests)
43. [Custom API Hook](#43-custom-api-hook)
44. [API Integration with Redux](#44-api-integration-with-redux)
45. [React Query / Server State](#45-react-query--server-state)
46. [Frontend and Backend Architecture](#46-frontend-and-backend-architecture)
47. [MERN API Example](#47-mern-api-example)
48. [Common API Mistakes](#48-common-api-mistakes)
49. [Most Asked Interview Questions](#49-most-asked-interview-questions)
50. [One-Minute Revision](#50-one-minute-revision)

---

# 1. What is an API?

API stands for **Application Programming Interface**.

It provides a way for different software systems to communicate.

For a MERN application:

```text
React Frontend
      ↓
     API
      ↓
Node + Express
      ↓
   MongoDB
```

Example:

```text
GET /api/products
```

The frontend requests products from the backend.

---

# 2. What is API Integration?

API integration means connecting the frontend application to backend services.

Example:

```text
React
 ↓
GET /api/products
 ↓
Express
 ↓
MongoDB
 ↓
Products JSON
 ↓
React
```

React can then display:

```jsx
products.map(product => (
  <ProductCard
    key={product._id}
    product={product}
  />
))
```

---

# 3. How Does React Communicate with a Backend?

React can use:

```text
fetch()
Axios
Other HTTP clients
```

Example:

```js
const response = await fetch(
  "http://localhost:5000/api/products"
);

const data = await response.json();
```

Or Axios:

```js
const response = await axios.get(
  "/api/products"
);

const data = response.data;
```

---

# 4. What is REST API?

REST stands for **Representational State Transfer**.

A REST API generally exposes resources through URLs and uses HTTP methods to operate on them.

Example:

```text
GET    /api/products
GET    /api/products/123
POST   /api/products
PATCH  /api/products/123
DELETE /api/products/123
```

Resource:

```text
products
```

---

# 5. HTTP Methods

The most common methods are:

| Method | Purpose                     |
| ------ | --------------------------- |
| GET    | Read data                   |
| POST   | Create data                 |
| PUT    | Replace/update a resource   |
| PATCH  | Partially update a resource |
| DELETE | Delete data                 |

Example:

```text
GET /api/users
POST /api/users
PATCH /api/users/10
DELETE /api/users/10
```

---

# 6. GET Request

GET is used to retrieve data.

Using Axios:

```js
const response = await axios.get(
  "/api/products"
);

console.log(response.data);
```

Using Fetch:

```js
const response = await fetch(
  "/api/products"
);

const data = await response.json();
```

---

# 7. POST Request

POST is commonly used to create a resource or trigger a server operation.

Axios:

```js
const response = await axios.post(
  "/api/products",
  {
    name: "React Book",
    price: 500
  }
);
```

The request body is:

```json
{
  "name": "React Book",
  "price": 500
}
```

---

# 8. PUT vs PATCH

### PUT

Usually represents replacing the resource representation.

```text
PUT /api/users/10
```

### PATCH

Usually represents a partial update.

```text
PATCH /api/users/10
```

Example:

```js
await axios.patch(
  `/api/users/${id}`,
  {
    name: "Anurag"
  }
);
```

Only the provided field needs to be changed, depending on the API implementation.

---

# 9. DELETE Request

Used to delete a resource.

```js
await axios.delete(
  `/api/products/${id}`
);
```

Backend:

```text
DELETE /api/products/:id
```

---

# 10. What is JSON?

JSON stands for **JavaScript Object Notation**.

It is commonly used for transferring structured data between frontend and backend.

Example:

```json
{
  "name": "React",
  "version": 19
}
```

API response:

```json
{
  "success": true,
  "data": {
    "name": "React"
  }
}
```

---

# 11. Fetch API

`fetch()` is a browser-provided API for making HTTP requests.

Example:

```js
const response = await fetch(
  "/api/products"
);

const data = await response.json();
```

For POST:

```js
const response = await fetch(
  "/api/products",
  {
    method: "POST",

    headers: {
      "Content-Type": "application/json"
    },

    body: JSON.stringify({
      name: "Book",
      price: 500
    })
  }
);
```

---

# 12. Axios

Axios is a popular HTTP client used in JavaScript applications.

Example:

```js
import axios from "axios";

const response = await axios.get(
  "/api/products"
);

console.log(response.data);
```

POST:

```js
await axios.post(
  "/api/products",
  {
    name: "Book",
    price: 500
  }
);
```

---

# 13. Fetch vs Axios

| Fetch                                          | Axios                                 |
| ---------------------------------------------- | ------------------------------------- |
| Built into browsers                            | External library                      |
| More manual setup                              | Convenient API                        |
| Does not reject automatically for HTTP 4xx/5xx | Rejects non-2xx responses by default  |
| JSON parsing is explicit                       | Response data is conveniently exposed |
| Supports AbortController                       | Supports AbortController              |
| Lightweight                                    | Rich client features                  |

Important interview point:

> With `fetch`, receiving a 404 or 500 does not by itself reject the promise. You should check `response.ok` or the status code.

Example:

```js
const response = await fetch("/api/products");

if (!response.ok) {
  throw new Error("Request failed");
}
```

---

# 14. async/await

API requests are asynchronous.

Instead of deeply nested `.then()` calls:

```js
fetch("/api/products")
  .then(response => response.json())
  .then(data => console.log(data))
  .catch(error => console.error(error));
```

we can use:

```js
try {
  const response = await fetch(
    "/api/products"
  );

  if (!response.ok) {
    throw new Error("Request failed");
  }

  const data = await response.json();

  console.log(data);
} catch (error) {
  console.error(error);
}
```

`async/await` makes asynchronous code easier to read.

---

# 15. API Call in useEffect

A common React pattern is fetching data when a component mounts.

```jsx
import { useEffect, useState } from "react";
import axios from "axios";

function Products() {
  const [products, setProducts] =
    useState([]);

  useEffect(() => {
    const fetchProducts = async () => {
      try {
        const response = await axios.get(
          "/api/products"
        );

        setProducts(response.data);
      } catch (error) {
        console.error(error);
      }
    };

    fetchProducts();
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

---

# 16. Loading State

Never assume an API request completes immediately.

Use a loading state:

```jsx
const [loading, setLoading] =
  useState(false);
```

Example:

```jsx
try {
  setLoading(true);

  const response =
    await axios.get("/api/products");

  setProducts(response.data);
} finally {
  setLoading(false);
}
```

UI:

```jsx
if (loading) {
  return <p>Loading...</p>;
}
```

---

# 17. Error Handling

Use a separate error state:

```jsx
const [error, setError] =
  useState(null);
```

Example:

```jsx
try {
  setLoading(true);
  setError(null);

  const response =
    await axios.get("/api/products");

  setProducts(response.data);
} catch (error) {
  setError(
    error.response?.data?.message ||
    "Something went wrong"
  );
} finally {
  setLoading(false);
}
```

Then:

```jsx
{error && (
  <p>{error}</p>
)}
```

---

# 18. Complete GET Example

```jsx
import {
  useEffect,
  useState
} from "react";

import axios from "axios";

function Products() {
  const [products, setProducts] =
    useState([]);

  const [loading, setLoading] =
    useState(true);

  const [error, setError] =
    useState(null);

  useEffect(() => {
    const fetchProducts = async () => {
      try {
        setLoading(true);
        setError(null);

        const response =
          await axios.get(
            "/api/products"
          );

        setProducts(response.data);
      } catch (error) {
        setError(
          error.response?.data?.message ||
          "Failed to fetch products"
        );
      } finally {
        setLoading(false);
      }
    };

    fetchProducts();
  }, []);

  if (loading) {
    return <p>Loading...</p>;
  }

  if (error) {
    return <p>{error}</p>;
  }

  return (
    <div>
      {products.map(product => (
        <div key={product._id}>
          {product.name}
        </div>
      ))}
    </div>
  );
}

export default Products;
```

---

# 19. POST API Example

Example registration form:

```jsx
const handleSubmit = async (e) => {
  e.preventDefault();

  try {
    const response = await axios.post(
      "/api/auth/register",
      {
        name,
        email,
        password
      }
    );

    console.log(response.data);
  } catch (error) {
    console.error(
      error.response?.data?.message
    );
  }
};
```

Flow:

```text
Form
 ↓
handleSubmit
 ↓
POST /api/auth/register
 ↓
Express Controller
 ↓
MongoDB
 ↓
Response
 ↓
React
```

---

# 20. CRUD Operations

CRUD means:

```text
Create
Read
Update
Delete
```

Example product API:

```text
POST   /api/products
GET    /api/products
GET    /api/products/:id
PATCH  /api/products/:id
DELETE /api/products/:id
```

React functions:

```js
const createProduct = data =>
  axios.post("/api/products", data);

const getProducts = () =>
  axios.get("/api/products");

const updateProduct = (id, data) =>
  axios.patch(`/api/products/${id}`, data);

const deleteProduct = id =>
  axios.delete(`/api/products/${id}`);
```

---

# 21. What is Axios Instance?

An Axios instance lets you create a reusable configured HTTP client.

Example:

```js
import axios from "axios";

const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL,
  timeout: 10000
});

export default api;
```

Then:

```js
api.get("/products");
api.post("/auth/login", data);
```

Advantages:

```text
Centralized base URL
Common timeout
Common headers
Interceptors
Reusable configuration
```

---

# 22. What are Axios Interceptors?

Interceptors allow you to run logic before requests or after responses.

Request interceptor:

```js
api.interceptors.request.use(
  config => {
    console.log(
      "Sending request..."
    );

    return config;
  }
);
```

Response interceptor:

```js
api.interceptors.response.use(
  response => response,

  error => {
    console.error(error);
    return Promise.reject(error);
  }
);
```

Common uses:

```text
Authentication
Logging
Global error handling
Refreshing credentials
Request metadata
```

---

# 23. Authentication with APIs

A common authentication flow:

```text
Login Form
    ↓
POST /api/auth/login
    ↓
Express
    ↓
Verify credentials
    ↓
Create session/token
    ↓
Response
    ↓
Frontend
```

After login:

```text
User
 ↓
Protected API
 ↓
Authentication check
 ↓
Authorized response
```

---

# 24. Cookies and API Requests

If your authentication architecture uses cookies, the browser needs to send credentials appropriately.

With Axios:

```js
const api = axios.create({
  baseURL:
    import.meta.env.VITE_API_URL,
  withCredentials: true
});
```

Then:

```js
await api.get("/api/auth/me");
```

On the backend, cookie and CORS configuration must also be correct.

---

# 25. Authorization Headers

Some APIs use an authorization header.

Example:

```js
const response = await axios.get(
  "/api/profile",
  {
    headers: {
      Authorization:
        `Bearer ${token}`
    }
  }
);
```

The backend can then verify the credential.

For browser applications, the exact token-storage architecture should be chosen carefully based on the application's security requirements.

---

# 26. Handling 401 Errors

HTTP `401 Unauthorized` generally means the request lacks valid authentication credentials.

For example:

```js
api.interceptors.response.use(
  response => response,

  error => {
    if (
      error.response?.status === 401
    ) {
      // Handle expired/invalid auth
    }

    return Promise.reject(error);
  }
);
```

Possible frontend behavior:

```text
401
 ↓
Clear invalid client auth state
 ↓
Redirect to login
```

The backend must remain responsible for actually enforcing authentication.

---

# 27. Environment Variables

Don't hardcode environment-specific API URLs throughout your application.

With Vite:

```env
VITE_API_URL=http://localhost:5000/api
```

Use:

```js
const api = axios.create({
  baseURL: import.meta.env.VITE_API_URL
});
```

Production might use a different value.

### Important

Frontend environment variables are generally **not secrets** because values exposed to client-side JavaScript can be inspected by users.

Never put private API keys or server secrets in frontend environment variables.

---

# 28. CORS

CORS stands for **Cross-Origin Resource Sharing**.

Suppose:

```text
Frontend:
http://localhost:5173

Backend:
http://localhost:5000
```

These are different origins.

The backend needs appropriate CORS configuration to allow the frontend to make browser requests.

Express example:

```js
import cors from "cors";

app.use(
  cors({
    origin: "http://localhost:5173",
    credentials: true
  })
);
```

The exact configuration depends on your authentication and deployment architecture.

---

# 29. Request Timeout

A request can take too long because of:

```text
Network problems
Server problems
Database delays
Third-party API problems
```

Axios example:

```js
const api = axios.create({
  baseURL:
    import.meta.env.VITE_API_URL,

  timeout: 10000
});
```

Here the request timeout is:

```text
10 seconds
```

---

# 30. Request Cancellation

Sometimes a component no longer needs a request.

For example:

```text
User searches:
react
rea
reac
```

Previous requests may become unnecessary.

With Fetch:

```js
const controller =
  new AbortController();

fetch("/api/products", {
  signal: controller.signal
});

controller.abort();
```

Cancellation can prevent unnecessary work and help avoid race-condition problems.

---

# 31. Race Conditions

Suppose the user searches:

```text
react
```

then immediately:

```text
redux
```

If the `react` request finishes after the `redux` request, its response could overwrite the newer results.

Conceptually:

```text
Request A → react
Request B → redux

B finishes first
A finishes later

Without protection:
A may overwrite B
```

Solutions include:

```text
AbortController
Request IDs
Libraries that manage server state
```

---

# 32. Search API

Frontend:

```js
const response =
  await api.get(
    `/products?search=${encodeURIComponent(search)}`
  );
```

Backend:

```text
GET /api/products?search=react
```

Express:

```js
const { search } = req.query;
```

Then the backend can query MongoDB.

---

# 33. Debounced Search

Without debouncing:

```text
r
re
rea
reac
react
```

could produce five API requests.

With debounce:

```text
User types
   ↓
Wait 300ms
   ↓
No new input?
   ↓
API request
```

Example custom hook:

```jsx
useEffect(() => {
  const timer = setTimeout(() => {
    searchProducts(search);
  }, 300);

  return () => clearTimeout(timer);
}, [search]);
```

This reduces unnecessary requests.

---

# 34. Pagination

Instead of requesting every product:

```text
10000 products
```

request a page:

```text
GET /api/products?page=2&limit=20
```

Backend:

```js
const page = Number(req.query.page) || 1;
const limit = Number(req.query.limit) || 20;

const skip = (page - 1) * limit;
```

Response:

```json
{
  "products": [],
  "page": 2,
  "limit": 20,
  "total": 10000
}
```

---

# 35. Filtering

Example:

```text
GET /api/products?category=books
```

Multiple filters:

```text
GET /api/products?category=books&minPrice=200&maxPrice=1000
```

React:

```js
const params = {
  category,
  minPrice,
  maxPrice
};

const response =
  await api.get("/products", {
    params
  });
```

Axios converts the `params` object into query parameters.

---

# 36. Sorting

Example:

```text
GET /api/products?sort=price_asc
```

Or:

```text
GET /api/products?sort=-createdAt
```

The backend determines how the sort parameter maps to database sorting.

---

# 37. File Upload

For image uploads:

```text
React
 ↓
FormData
 ↓
POST multipart/form-data
 ↓
Express/Multer
 ↓
Cloudinary
 ↓
Image URL
 ↓
MongoDB
```

Frontend:

```js
const formData =
  new FormData();

formData.append(
  "image",
  file
);

formData.append(
  "name",
  name
);

await api.post(
  "/products",
  formData
);
```

---

# 38. FormData

`FormData` is useful when sending files.

Example:

```js
const formData =
  new FormData();

formData.append(
  "title",
  title
);

formData.append(
  "image",
  imageFile
);
```

With Axios:

```js
await api.post(
  "/products",
  formData
);
```

You normally don't need to manually set the multipart `Content-Type` header in the browser; Axios/browser handling can set the correct boundary.

---

# 39. API Response Structure

A consistent response format makes frontend development easier.

Example:

```json
{
  "success": true,
  "message": "Products fetched successfully",
  "data": []
}
```

Error:

```json
{
  "success": false,
  "message": "Product not found"
}
```

Frontend:

```js
if (response.data.success) {
  setProducts(response.data.data);
}
```

Consistency is more important than one specific response shape.

---

# 40. Optimistic Updates

An optimistic update changes the UI **before the server confirms success**.

Example:

```text
User likes post
      ↓
UI immediately shows Like
      ↓
API request
      ↓
Success → keep change

Failure → rollback
```

Useful for:

```text
Likes
Bookmarks
Cart quantity
Simple toggles
```

The rollback logic is important because the server can reject the operation.

---

# 41. Retrying API Requests

Some temporary failures may be retryable.

Examples:

```text
Temporary network error
Transient service failure
```

But don't blindly retry every request.

For example:

```text
GET → often safe to retry

POST → may create duplicate resources
```

Retry logic should consider:

```text
HTTP method
Idempotency
Error type
Retry count
Backoff
```

---

# 42. Avoiding Duplicate API Requests

Duplicate requests can happen because of:

```text
Multiple clicks
Component lifecycle
Strict Mode development behavior
Repeated effects
Multiple components fetching same data
```

Solutions:

```text
Disable submit button while submitting
Use proper effect dependencies
Cancel obsolete requests
Cache server data
Use request deduplication
```

Example:

```jsx
<button
  disabled={loading}
  onClick={handleSubmit}
>
  {loading
    ? "Submitting..."
    : "Submit"}
</button>
```

---

# 43. Custom API Hook

Repeated API logic can be extracted into a custom hook.

Example:

```jsx
function useFetch(url) {
  const [data, setData] =
    useState(null);

  const [loading, setLoading] =
    useState(true);

  const [error, setError] =
    useState(null);

  useEffect(() => {
    const fetchData = async () => {
      try {
        setLoading(true);

        const response =
          await axios.get(url);

        setData(response.data);
      } catch (error) {
        setError(error);
      } finally {
        setLoading(false);
      }
    };

    fetchData();
  }, [url]);

  return {
    data,
    loading,
    error
  };
}
```

Usage:

```jsx
const {
  data,
  loading,
  error
} = useFetch("/api/products");
```

---

# 44. API Integration with Redux

Redux can manage API-related client state.

Example:

```text
Component
    ↓
dispatch(fetchProducts())
    ↓
Thunk
    ↓
API
    ↓
pending
    ↓
fulfilled / rejected
    ↓
Redux Store
    ↓
Component
```

With Redux Toolkit:

```js
createAsyncThunk()
```

is commonly used for this pattern.

---

# 45. React Query / Server State

For complex server-state requirements, a dedicated data-fetching/cache library can be useful.

Such tools can help with:

```text
Caching
Refetching
Request deduplication
Stale data
Loading states
Error states
Invalidation
Pagination
```

This is different from ordinary local UI state.

### Interview Answer

> I don't automatically put all API data into Redux. If the application has complex server-state requirements, I would consider a dedicated server-state solution.

---

# 46. Frontend and Backend Architecture

A clean MERN architecture might look like:

```text
React
 │
 ├── Components
 ├── Pages
 ├── Hooks
 └── API Layer
          │
          ↓
       Axios
          │
          ↓
    Express Routes
          │
          ↓
    Controllers
          │
          ↓
      Services
          │
          ↓
      Mongoose
          │
          ↓
      MongoDB
```

This separation keeps API logic from becoming scattered across components.

---

# 47. MERN API Example

Suppose you have a civic issue reporting application.

Frontend:

```js
const response =
  await api.post(
    "/complaints",
    {
      title,
      description,
      latitude,
      longitude
    }
  );
```

Backend:

```text
POST /api/complaints
        ↓
Express Route
        ↓
Complaint Controller
        ↓
Validation
        ↓
AI Analysis
        ↓
MongoDB
        ↓
Response
```

The response could be:

```json
{
  "success": true,
  "complaint": {
    "category": "Road Damage",
    "priority": "High",
    "summary": "A pothole was reported on the main road."
  }
}
```

React then updates the UI.

---

# 48. Common API Mistakes

## Mistake 1 — No loading state

Bad:

```jsx
return products.map(...);
```

Better:

```jsx
if (loading) {
  return <Loader />;
}
```

---

## Mistake 2 — No error handling

Bad:

```js
const response =
  await api.get("/products");
```

Better:

```js
try {
  const response =
    await api.get("/products");
} catch (error) {
  // Handle error
}
```

---

## Mistake 3 — Hardcoding URLs everywhere

Bad:

```js
axios.get(
  "http://localhost:5000/api/products"
);
```

Better:

```js
api.get("/products");
```

with a configured Axios instance.

---

## Mistake 4 — Putting secrets in frontend code

Never put:

```text
Database passwords
Private API keys
JWT signing secrets
Cloud provider private credentials
```

in frontend code.

---

## Mistake 5 — Trusting frontend validation

Frontend validation improves UX:

```text
Email required
Password required
```

But backend validation is still required because clients can bypass frontend code.

---

## Mistake 6 — Exposing sensitive information in errors

Avoid returning internal server details such as:

```text
Database connection strings
Stack traces
Private configuration
```

to production clients.

---

# 49. Most Asked Interview Questions

## ⭐ Basic

1. What is an API?
2. What is API integration?
3. What is REST API?
4. What are HTTP methods?
5. GET vs POST?
6. PUT vs PATCH?
7. What is DELETE?
8. What is JSON?
9. What is `fetch()`?
10. What is Axios?

## ⭐ React

11. How do you call an API in React?
12. Why use `useEffect()` for fetching?
13. How do you handle loading state?
14. How do you handle API errors?
15. How do you prevent duplicate requests?
16. How do you cancel API requests?
17. What are race conditions?
18. How do you implement search?
19. How do you debounce API calls?
20. How do you implement pagination?

## ⭐ Axios

21. What is an Axios instance?
22. What are Axios interceptors?
23. How do you configure a base URL?
24. How do you send query parameters?
25. How do you send FormData?
26. How do you handle 401 errors?
27. How do you set a timeout?

## ⭐ Authentication

28. How does frontend authentication work?
29. How are cookies sent with Axios?
30. What is `withCredentials`?
31. What is an Authorization header?
32. What is a 401 response?
33. Why can't frontend route/API checks replace backend authorization?

## ⭐ MERN

34. How does React communicate with Express?
35. How does Express communicate with MongoDB?
36. How do you implement CRUD?
37. How do you upload images?
38. How do you use Cloudinary?
39. How do you implement pagination?
40. How do you implement search and filtering?

---

# 50. One-Minute Revision

Remember:

```text
React
  ↓
Axios / Fetch
  ↓
HTTP Request
  ↓
Express API
  ↓
Controller
  ↓
MongoDB
  ↓
JSON Response
  ↓
React State
  ↓
UI
```

HTTP:

```text
GET
 ↓
Read

POST
 ↓
Create

PUT
 ↓
Replace

PATCH
 ↓
Partial Update

DELETE
 ↓
Delete
```

React API state:

```text
loading
   ↓
request
   ↓
success / error
```

Axios:

```text
axios.create()
      ↓
baseURL
      ↓
interceptors
      ↓
API calls
```

Authentication:

```text
Login
 ↓
Backend authentication
 ↓
Session/token mechanism
 ↓
Protected API
 ↓
Backend authorization
```

---

# 🎯 Interview Formula

When asked:

> How do you integrate an API into a React application?

A strong answer:

> I usually create a centralized API layer using Axios or Fetch. I configure the base URL through environment configuration and keep API calls separate from presentation components where practical. For each request I handle loading, success, and error states. For authenticated requests, I use the application's chosen authentication mechanism, such as secure cookies or authorization headers. I also handle HTTP errors, cancellation where useful, and prevent duplicate requests. For larger applications, I may use Redux Toolkit or a dedicated server-state library depending on the application's requirements.

---

# 🚀 Real MERN Example

For an e-commerce application:

```text
                    React
                      │
                 API Layer
                      │
                    Axios
                      │
          ┌───────────┼───────────┐
          ↓           ↓           ↓
       Products      Cart       Auth
          │           │           │
          └───────────┼───────────┘
                      ↓
                Express.js
                      │
                 Middleware
                      │
                 Controllers
                      │
                  Mongoose
                      │
                  MongoDB
```

Example endpoints:

```text
GET    /api/products
GET    /api/products/:id
POST   /api/products
PATCH  /api/products/:id
DELETE /api/products/:id

POST   /api/auth/login
POST   /api/auth/register
GET    /api/auth/me

GET    /api/cart
POST   /api/cart
PATCH  /api/cart/:id
DELETE /api/cart/:id
```

This is the basic **React → API → Express → MongoDB → React** architecture you should be able to explain in a MERN interview.
