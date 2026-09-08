# Top 50 Node.js Interview Questions & Answers

A collection of the **top 50 Node.js, Express.js, and backend interview questions** for MERN Stack interviews.

---

# 1. What is Node.js?

Node.js is a JavaScript runtime environment that allows us to run JavaScript outside the browser, mainly for backend development.

It is built on Google's **V8 JavaScript engine** and uses an **event-driven, non-blocking I/O model**.

### Example

```js
const http = require("http");

const server = http.createServer((req, res) => {
    res.end("Hello World");
});

server.listen(3000);
```

---

# 2. Why is Node.js used for backend development?

Node.js is commonly used for backend development because:

* JavaScript can be used for both frontend and backend.
* It uses non-blocking I/O.
* It is efficient for I/O-intensive applications.
* It has a large npm ecosystem.
* It is suitable for REST APIs and real-time applications.

---

# 3. What are the advantages of Node.js?

### Advantages

1. Fast execution using the V8 engine.
2. Non-blocking architecture.
3. Good for real-time applications.
4. Huge npm ecosystem.
5. Same language can be used on frontend and backend.
6. Easy to build REST APIs.

---

# 4. What are the disadvantages of Node.js?

### Disadvantages

* CPU-intensive tasks can block the main JavaScript thread.
* Not ideal for heavy computational operations on the main thread.
* Poorly designed asynchronous code can become difficult to maintain.
* Developers need a good understanding of asynchronous programming.

---

# 5. Is Node.js single-threaded?

Yes, Node.js executes JavaScript on a **single main thread**.

However, Node.js internally can use multiple threads through its runtime and thread pool for certain operations.

For example, some file-system operations can be handled using the underlying thread pool.

### Interview Answer

> Node.js is single-threaded for executing JavaScript, but it can use background threads for certain asynchronous operations.

---

# 6. What is the V8 engine?

V8 is Google's open-source JavaScript engine.

It is used by:

* Google Chrome
* Node.js

V8 converts JavaScript code into machine code and executes it.

---

# 7. What is the Event Loop?

The Event Loop is a mechanism that allows Node.js to handle asynchronous operations without blocking the main JavaScript thread.

### Example

```js
console.log("Start");

setTimeout(() => {
    console.log("Timer");
}, 0);

console.log("End");
```

### Output

```text
Start
End
Timer
```

The synchronous code executes first, while the timer callback is handled later.

---

# 8. What is non-blocking I/O?

Non-blocking I/O means Node.js does not wait for an I/O operation to finish before continuing with other work.

For example:

```js
fs.readFile("data.txt", "utf8", (err, data) => {
    console.log(data);
});

console.log("Other work");
```

Node.js can continue executing `"Other work"` while the file is being read.

---

# 9. What is synchronous vs asynchronous code?

## Synchronous

The program waits for the operation to complete.

```js
const data = fs.readFileSync("data.txt");

console.log(data);
```

## Asynchronous

The program can continue executing while the operation is being completed.

```js
fs.readFile("data.txt", (err, data) => {
    console.log(data);
});

console.log("Continue");
```

---

# 10. How can Node.js handle many requests if it is single-threaded?

Node.js uses an **event-driven and non-blocking architecture**.

Instead of creating a new JavaScript thread for every request, Node.js uses the Event Loop and delegates asynchronous I/O operations.

### Interview Answer

> Node.js can handle many concurrent I/O operations because it doesn't block the main thread while waiting for I/O. It delegates asynchronous work and processes callbacks when the operations complete.

---

# 11. What is a callback?

A callback is a function passed as an argument to another function and executed later.

### Example

```js
function greet(name, callback) {
    console.log("Hello " + name);

    callback();
}

greet("Anurag", () => {
    console.log("Done");
});
```

---

# 12. What is callback hell?

Callback hell occurs when multiple asynchronous operations are nested inside one another.

### Example

```js
getUser(() => {
    getOrders(() => {
        getProducts(() => {
            // deeply nested code
        });
    });
});
```

This makes the code difficult to read and maintain.

### Solutions

* Promises
* `async/await`
* Breaking code into separate functions

---

# 13. What is a Promise?

A Promise represents the eventual completion or failure of an asynchronous operation.

A Promise has three states:

```text
Pending
   ↓
Fulfilled
   OR
Rejected
```

### Example

```js
fetchData()
    .then(data => {
        console.log(data);
    })
    .catch(error => {
        console.log(error);
    });
```

---

# 14. What is async/await?

`async/await` provides a cleaner way to work with Promises.

### Example

```js
async function getUser() {
    try {
        const user = await User.findById(id);

        console.log(user);
    } catch (error) {
        console.log(error);
    }
}
```

It makes asynchronous code easier to read.

---

# 15. Difference between Promise and async/await?

Both are used to handle asynchronous operations.

### Promise

```js
getUser()
    .then(user => console.log(user))
    .catch(error => console.log(error));
```

### async/await

```js
try {
    const user = await getUser();

    console.log(user);
} catch (error) {
    console.log(error);
}
```

`async/await` is syntax built around Promises and usually makes asynchronous code easier to read.

---

# 16. What is process.nextTick()?

`process.nextTick()` schedules a callback to execute after the current operation completes, before the Event Loop proceeds to later phases.

### Example

```js
console.log("A");

process.nextTick(() => {
    console.log("B");
});

console.log("C");
```

### Output

```text
A
C
B
```

---

# 17. What is setTimeout()?

`setTimeout()` schedules a callback to execute after at least the specified delay.

```js
setTimeout(() => {
    console.log("Hello");
}, 1000);
```

The callback becomes eligible after approximately 1 second. It does not guarantee exact execution at that time.

---

# 18. What is setImmediate()?

`setImmediate()` schedules a callback to execute during the Event Loop's **check phase**.

It is commonly useful for scheduling work after the current I/O callbacks.

---

# 19. Difference between setTimeout() and setImmediate()?

```js
setTimeout(() => {
    console.log("Timeout");
}, 0);

setImmediate(() => {
    console.log("Immediate");
});
```

Their execution order can depend on where the code is executed.

Inside an I/O callback, `setImmediate()` generally executes before `setTimeout(..., 0)`.

---

# 20. What are microtasks?

Microtasks are callbacks that are processed with high priority between Event Loop phases.

Examples include:

```js
Promise.then()
queueMicrotask()
process.nextTick()
```

In Node.js, `process.nextTick()` has its own higher-priority queue.

---

# 21. What are modules in Node.js?

A module is a reusable piece of code that contains related functionality.

### Example

```js
// math.js

function add(a, b) {
    return a + b;
}

module.exports = add;
```

Use it:

```js
const add = require("./math");

console.log(add(2, 3));
```

---

# 22. What is CommonJS?

CommonJS is a module system commonly used in Node.js.

### Import

```js
const express = require("express");
```

### Export

```js
module.exports = router;
```

---

# 23. What are ES Modules?

ES Modules are JavaScript's standard module system.

### Import

```js
import express from "express";
```

### Export

```js
export default router;
```

---

# 24. Difference between require() and import?

### CommonJS

```js
const express = require("express");
```

### ES Modules

```js
import express from "express";
```

`require()` is associated with CommonJS, while `import/export` is the standard ES Module syntax.

---

# 25. Difference between module.exports and exports?

Initially:

```js
exports === module.exports
```

Therefore this works:

```js
exports.add = add;
```

But:

```js
exports = add;
```

does not replace the actual exported value.

To replace the entire exported value:

```js
module.exports = add;
```

---

# 26. What are built-in Node.js modules?

Node.js provides several built-in modules.

Common examples:

```text
fs
path
http
os
events
crypto
url
stream
```

Example:

```js
const fs = require("fs");
```

---

# 27. What is the fs module?

`fs` stands for **File System**.

It is used to work with files and directories.

Example:

```js
const fs = require("fs");

fs.readFile("data.txt", "utf8", (err, data) => {
    if (err) {
        console.log(err);
        return;
    }

    console.log(data);
});
```

---

# 28. What is the path module?

The `path` module provides utilities for working with file and directory paths.

Example:

```js
const path = require("path");

const filePath = path.join(__dirname, "files", "data.txt");

console.log(filePath);
```

---

# 29. What is the http module?

The `http` module allows us to create HTTP servers without using Express.

Example:

```js
const http = require("http");

const server = http.createServer((req, res) => {
    res.end("Hello World");
});

server.listen(3000);
```

---

# 30. What is the events module?

The `events` module allows Node.js applications to work with event-driven programming.

Example:

```js
const EventEmitter = require("events");

const emitter = new EventEmitter();

emitter.on("login", () => {
    console.log("User logged in");
});

emitter.emit("login");
```

---

# 31. What is npm?

npm stands for **Node Package Manager**.

It is used to:

* Install packages
* Manage dependencies
* Run scripts
* Publish packages

Example:

```bash
npm install express
```

---

# 32. What is package.json?

`package.json` contains information about a Node.js project.

It can contain:

* Project name
* Version
* Dependencies
* Scripts
* Project metadata

Example:

```json
{
    "name": "backend",
    "scripts": {
        "start": "node server.js",
        "dev": "nodemon server.js"
    }
}
```

---

# 33. Difference between dependencies and devDependencies?

## dependencies

Packages required by the application.

```bash
npm install express
```

## devDependencies

Packages mainly required during development.

```bash
npm install -D nodemon
```

---

# 34. What is package-lock.json?

`package-lock.json` records the exact dependency tree installed for a project.

It helps ensure that different developers and environments install consistent versions of dependencies.

---

# 35. What is nodemon?

Nodemon is a development tool that automatically restarts the Node.js application when files change.

Example:

```bash
npx nodemon server.js
```

---

# 36. What is Express.js?

Express.js is a lightweight web framework built on top of Node.js.

It provides features such as:

* Routing
* Middleware
* Request handling
* Response handling
* Error handling

### Example

```js
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello World");
});

app.listen(3000);
```

---

# 37. Why use Express instead of Node's HTTP module?

Using the Node.js HTTP module directly requires more manual code for routing and request handling.

Express provides:

* Easy routing
* Middleware
* Request/response helpers
* Error handling
* Cleaner API structure

Therefore, Express makes backend development easier and faster.

---

# 38. What is middleware in Express?

Middleware is a function that has access to:

```text
request
response
next
```

It can:

* Execute code
* Modify request/response
* End the request
* Call the next middleware

### Example

```js
const authMiddleware = (req, res, next) => {
    console.log("Authentication checking...");

    next();
};

app.use(authMiddleware);
```

---

# 39. What are the types of middleware?

Common types are:

1. Application-level middleware
2. Router-level middleware
3. Built-in middleware
4. Third-party middleware
5. Error-handling middleware

### Example

```js
app.use(express.json());
```

`express.json()` is built-in middleware.

---

# 40. What is next() in Express?

`next()` passes control to the next middleware or route handler.

Example:

```js
app.use((req, res, next) => {
    console.log("Middleware executed");

    next();
});
```

If middleware neither sends a response nor calls `next()`, the request may remain hanging.

---

# 41. What is routing in Express?

Routing defines how an application responds to a particular HTTP method and URL.

Example:

```js
app.get("/users", getUsers);

app.post("/users", createUser);

app.put("/users/:id", updateUser);

app.delete("/users/:id", deleteUser);
```

---

# 42. Difference between GET and POST?

## GET

Used mainly to retrieve data.

```http
GET /users
```

## POST

Used mainly to create or submit data.

```http
POST /users
```

Request body:

```json
{
    "name": "Anurag"
}
```

---

# 43. Difference between req.params, req.query and req.body?

This is one of the most important Express interview questions.

## req.params

Used for URL parameters.

```http
GET /users/123
```

```js
req.params.id
```

Result:

```text
123
```

---

## req.query

Used for query parameters.

```http
GET /users?role=admin
```

```js
req.query.role
```

Result:

```text
admin
```

---

## req.body

Used to access data sent in the request body.

```http
POST /users
```

```json
{
    "name": "Anurag"
}
```

Access:

```js
req.body.name
```

---

# 44. What is error-handling middleware?

Error-handling middleware handles errors in an Express application.

It has four parameters:

```js
app.use((err, req, res, next) => {
    console.error(err);

    res.status(500).json({
        message: err.message
    });
});
```

The important difference is:

```js
(err, req, res, next)
```

---

# 45. How do you handle errors in Express?

A common approach is centralized error handling.

```js
app.use((err, req, res, next) => {
    console.error(err);

    res.status(err.statusCode || 500).json({
        success: false,
        message: err.message || "Internal Server Error"
    });
});
```

Errors can be passed using:

```js
next(error);
```

---

# 46. What is JWT?

JWT stands for **JSON Web Token**.

It is commonly used for authentication.

After successful login:

```text
User Login
    ↓
Verify Email & Password
    ↓
Generate JWT
    ↓
Send Token
    ↓
Client sends Token
    ↓
Server verifies Token
    ↓
Allow / Reject Request
```

Example:

```js
const token = jwt.sign(
    { userId: user._id },
    process.env.JWT_SECRET,
    { expiresIn: "1d" }
);
```

---

# 47. Authentication vs Authorization?

## Authentication

Authentication answers:

> "Who are you?"

Example:

```text
Login with email + password
```

## Authorization

Authorization answers:

> "What are you allowed to do?"

Example:

```text
Admin → Delete users
User → Cannot delete users
```

### Simple difference

```text
Authentication = Identity

Authorization = Permission
```

---

# 48. What is CORS?

CORS stands for **Cross-Origin Resource Sharing**.

It controls whether a browser allows a frontend from one origin to access resources from another origin.

Example:

```text
Frontend:
http://localhost:5173

Backend:
http://localhost:5000
```

These are different origins.

In Express:

```js
const cors = require("cors");

app.use(cors({
    origin: "http://localhost:5173",
    credentials: true
}));
```

---

# 49. What are HttpOnly, Secure and SameSite cookies?

These are cookie security attributes.

### HttpOnly

```text
HttpOnly
```

Prevents JavaScript from directly accessing the cookie.

This helps reduce the risk of cookie theft through XSS.

### Secure

```text
Secure
```

The cookie is sent only over HTTPS.

### SameSite

Controls when cookies are sent in cross-site requests.

Common values:

```text
Strict
Lax
None
```

---

# 50. How would you design a secure login/signup API?

A typical secure authentication flow:

```text
                SIGNUP
                  ↓
        Validate user input
                  ↓
          Hash password
                  ↓
          Save user in DB
                  ↓
                LOGIN
                  ↓
       Find user by email
                  ↓
       Compare password hash
                  ↓
            Generate JWT
                  ↓
       Store/send secure cookie
                  ↓
       Authentication Middleware
                  ↓
          Verify JWT
                  ↓
        Access protected route
```

### Example

```js
const bcrypt = require("bcrypt");
const jwt = require("jsonwebtoken");

const hashedPassword = await bcrypt.hash(password, 10);

const isMatch = await bcrypt.compare(
    password,
    user.password
);

const token = jwt.sign(
    { userId: user._id },
    process.env.JWT_SECRET,
    { expiresIn: "1d" }
);
```

For a browser-based application, an **HttpOnly cookie** can be used to reduce JavaScript access to the token.

---

# ⭐ Most Important Questions for MERN Interviews

If you have limited time, prioritize these:

| Priority | Topic                                 |
| -------- | ------------------------------------- |
| ⭐⭐⭐⭐⭐    | Event Loop                            |
| ⭐⭐⭐⭐⭐    | Single-threaded architecture          |
| ⭐⭐⭐⭐⭐    | Middleware                            |
| ⭐⭐⭐⭐⭐    | JWT Authentication                    |
| ⭐⭐⭐⭐⭐    | `req.params`, `req.query`, `req.body` |
| ⭐⭐⭐⭐⭐    | CORS                                  |
| ⭐⭐⭐⭐⭐    | Error Handling                        |
| ⭐⭐⭐⭐⭐    | async/await                           |
| ⭐⭐⭐⭐     | Promises                              |
| ⭐⭐⭐⭐     | Cookies                               |
| ⭐⭐⭐⭐     | Authentication vs Authorization       |
| ⭐⭐⭐⭐     | Express Routing                       |
| ⭐⭐⭐⭐     | CommonJS vs ES Modules                |
| ⭐⭐⭐      | npm                                   |
| ⭐⭐⭐      | Node.js built-in modules              |

---

# 🎯 Project-Based Follow-up Questions

After these 50 questions, interviewers often ask questions based on your MERN projects.

Prepare these as well:

1. How did you structure your Node.js project?
2. Why did you choose Express.js?
3. How did you implement JWT authentication?
4. Where did you store your JWT?
5. How did you implement role-based authorization?
6. How did you handle errors?
7. How did you validate API requests?
8. How did you implement file uploads?
9. How did you use Cloudinary?
10. How did you solve CORS issues?
11. How did you connect Node.js with MongoDB?
12. Why did you use Mongoose?
13. What is a Mongoose schema?
14. What is a Mongoose model?
15. How did you optimize your API?
16. How did you implement pagination?
17. How did you implement search?
18. How did you implement filtering?
19. How did you implement real-time updates using Socket.IO?
20. How did you improve API performance?
21. Where did you deploy your backend?
22. How did you manage environment variables?
23. How did you protect API endpoints?
24. How did you test APIs using Postman?
25. Explain one complete API from your project from frontend → backend → database → response.

---

# 🚀 Recommended Preparation Order

For a MERN backend interview, study in this order:

```text
JavaScript Async Concepts
        ↓
Node.js Basics
        ↓
Event Loop
        ↓
Express.js
        ↓
Middleware
        ↓
REST APIs
        ↓
MongoDB + Mongoose
        ↓
Authentication + JWT
        ↓
Authorization / RBAC
        ↓
CORS + Cookies
        ↓
Error Handling
        ↓
File Uploads
        ↓
Socket.IO
        ↓
Redis / Caching
        ↓
Deployment
```

This order will help you understand **why Node.js works the way it does**, instead of only memorizing interview definitions.
