# JavaScript Interview Questions & Answers — Top 50

A collection of the **50 most important JavaScript interview questions** for beginners, experienced developers, and MERN Stack developers.

---

## Table of Contents

1. [What is JavaScript?](#1-what-is-javascript)
2. [var vs let vs const](#2-what-is-the-difference-between-var-let-and-const)
3. [JavaScript Data Types](#3-what-are-the-data-types-in-javascript)
4. [Primitive vs Reference Types](#4-primitive-vs-reference-data-types)
5. [Type Coercion](#5-what-is-type-coercion)
6. [== vs ===](#6-what-is-the-difference-between--and-)
7. [null vs undefined](#7-what-is-the-difference-between-null-and-undefined)
8. [NaN](#8-what-is-nan)
9. [Hoisting](#9-what-is-hoisting)
10. [Temporal Dead Zone](#10-what-is-the-temporal-dead-zone)
11. [Function Declaration vs Expression](#11-function-declaration-vs-function-expression)
12. [Arrow Functions](#12-what-are-arrow-functions)
13. [Arrow Function vs Normal Function](#13-arrow-function-vs-normal-function)
14. [Scope](#14-what-is-scope)
15. [Lexical Scope](#15-what-is-lexical-scope)
16. [Closure](#16-what-is-a-closure)
17. [Higher-Order Functions](#17-what-are-higher-order-functions)
18. [Callback Functions](#18-what-is-a-callback-function)
19. [IIFE](#19-what-is-an-iife)
20. [Objects](#20-what-is-an-object)
21. [Shallow vs Deep Copy](#21-shallow-copy-vs-deep-copy)
22. [Clone an Object](#22-how-do-you-clone-an-object)
23. [Destructuring](#23-what-is-destructuring)
24. [Spread Operator](#24-what-is-the-spread-operator)
25. [Rest Operator](#25-what-is-the-rest-operator)
26. [map vs filter vs reduce](#26-map-vs-filter-vs-reduce)
27. [forEach vs map](#27-foreach-vs-map)
28. [find vs filter](#28-find-vs-filter)
29. [Optional Chaining](#29-what-is-optional-chaining)
30. [Nullish Coalescing](#30-what-is-nullish-coalescing)
31. [this Keyword](#31-what-is-the-this-keyword)
32. [this in Arrow Functions](#32-how-does-this-behave-in-arrow-functions)
33. [call, apply, bind](#33-what-are-call-apply-and-bind)
34. [Prototype](#34-what-is-a-prototype)
35. [Prototypal Inheritance](#35-what-is-prototypal-inheritance)
36. [Prototype Chain](#36-what-is-the-prototype-chain)
37. [Classes](#37-what-are-classes-in-javascript)
38. [Getters and Setters](#38-what-are-getters-and-setters)
39. [Event Bubbling](#39-what-is-event-bubbling)
40. [Event Capturing](#40-what-is-event-capturing)
41. [Synchronous vs Asynchronous](#41-synchronous-vs-asynchronous-javascript)
42. [Event Loop](#42-what-is-the-event-loop)
43. [Call Stack and Callback Queue](#43-call-stack-and-callback-queue)
44. [Promise](#44-what-is-a-promise)
45. [Promise States](#45-what-are-the-states-of-a-promise)
46. [Promise.all and Others](#46-promiseall-promiseallsettled-promiserace-and-promiseany)
47. [async/await](#47-what-is-asyncawait)
48. [async/await vs then](#48-asyncawait-vs-then)
49. [Debouncing vs Throttling](#49-debouncing-vs-throttling)
50. [CommonJS vs ES Modules](#50-commonjs-vs-es-modules)

---

# 1. What is JavaScript?

JavaScript is a **high-level, dynamically typed programming language** mainly used to create interactive web applications.

It can run:

* In browsers
* On servers using Node.js
* In mobile applications
* In desktop applications

### Example

```javascript
const name = "Anurag";

console.log(`Hello ${name}`);
```

JavaScript is one of the core technologies of the web along with HTML and CSS.

---

# 2. What is the difference between var, let, and const?

All three are used to declare variables, but they behave differently.

| Feature       | var      | let   | const |
| ------------- | -------- | ----- | ----- |
| Scope         | Function | Block | Block |
| Redeclaration | Yes      | No    | No    |
| Reassignment  | Yes      | Yes   | No    |
| Hoisted       | Yes      | Yes   | Yes   |
| TDZ           | No       | Yes   | Yes   |

### Example

```javascript
var a = 10;
var a = 20; // Allowed

let b = 10;
b = 20; // Allowed

const c = 10;
// c = 20; // Error
```

### Interview Answer

> `var` is function-scoped, while `let` and `const` are block-scoped. `let` allows reassignment, whereas `const` does not allow reassignment.

---

# 3. What are the Data Types in JavaScript?

JavaScript has **primitive** and **non-primitive/reference** data types.

### Primitive

```text
String
Number
Boolean
Undefined
Null
BigInt
Symbol
```

### Non-Primitive

```text
Object
Array
Function
```

### Example

```javascript
let name = "Anurag";       // String
let age = 21;              // Number
let active = true;         // Boolean
let x;                     // Undefined
let y = null;              // Null
let big = 123n;            // BigInt
```

---

# 4. Primitive vs Reference Data Types

### Primitive

Primitive values store the actual value.

```javascript
let a = 10;
let b = a;

b = 20;

console.log(a); // 10
console.log(b); // 20
```

### Reference

Objects store a reference to the object.

```javascript
let obj1 = { name: "Anurag" };
let obj2 = obj1;

obj2.name = "Rahul";

console.log(obj1.name); // Rahul
```

### Interview Answer

> Primitive values are copied by value, while objects and arrays are accessed through references.

---

# 5. What is Type Coercion?

Type coercion means JavaScript automatically converts one data type into another.

### Example

```javascript
console.log("5" + 2);
```

Output:

```text
52
```

Because `2` is converted into a string.

Another example:

```javascript
console.log("5" - 2);
```

Output:

```text
3
```

Here `"5"` is converted into a number.

---

# 6. What is the difference between == and ===?

### `==`

Performs comparison after type conversion.

```javascript
console.log(5 == "5"); // true
```

### `===`

Checks both value and data type.

```javascript
console.log(5 === "5"); // false
```

### Interview Answer

> `==` performs loose equality and may perform type coercion, whereas `===` performs strict equality without type coercion.

**Prefer `===` in most cases.**

---

# 7. What is the difference between null and undefined?

### undefined

A variable has been declared but has not been assigned a value.

```javascript
let x;

console.log(x); // undefined
```

### null

`null` represents an intentional absence of a value.

```javascript
let user = null;
```

### Interview Answer

> `undefined` generally means a value has not been assigned, while `null` is explicitly assigned to represent no value.

---

# 8. What is NaN?

`NaN` means **Not a Number**.

It occurs when a mathematical operation cannot produce a valid number.

```javascript
console.log("hello" * 5);
```

Output:

```text
NaN
```

You can check it using:

```javascript
Number.isNaN(value);
```

Example:

```javascript
console.log(Number.isNaN(NaN)); // true
```

---

# 9. What is Hoisting?

Hoisting is JavaScript's behavior where declarations are processed before code execution.

### var

```javascript
console.log(a);

var a = 10;
```

Output:

```text
undefined
```

Conceptually:

```javascript
var a;

console.log(a);

a = 10;
```

### Function Declaration

Function declarations can be called before they appear in the code.

```javascript
hello();

function hello() {
    console.log("Hello");
}
```

Output:

```text
Hello
```

---

# 10. What is the Temporal Dead Zone?

The Temporal Dead Zone (TDZ) is the period between entering a scope and the point where a `let` or `const` variable is initialized.

```javascript
console.log(x);

let x = 10;
```

This produces:

```text
ReferenceError
```

Although `x` is hoisted, it cannot be accessed before initialization.

---

# 11. Function Declaration vs Function Expression

### Function Declaration

```javascript
function add(a, b) {
    return a + b;
}
```

It can be called before its declaration.

### Function Expression

```javascript
const add = function(a, b) {
    return a + b;
};
```

It cannot be used before initialization.

---

# 12. What are Arrow Functions?

Arrow functions provide a shorter syntax for writing functions.

### Normal Function

```javascript
function add(a, b) {
    return a + b;
}
```

### Arrow Function

```javascript
const add = (a, b) => {
    return a + b;
};
```

Short form:

```javascript
const add = (a, b) => a + b;
```

---

# 13. Arrow Function vs Normal Function

Important differences:

### 1. `this`

Arrow functions do not have their own `this`.

### 2. arguments

Arrow functions do not have their own `arguments` object.

### 3. Constructor

Arrow functions cannot be used with `new`.

### Example

```javascript
const user = {
    name: "Anurag",

    normal: function() {
        console.log(this.name);
    },

    arrow: () => {
        console.log(this.name);
    }
};

user.normal(); // Anurag
user.arrow();  // undefined (in typical module/browser contexts)
```

---

# 14. What is Scope?

Scope determines where a variable can be accessed.

JavaScript has:

* Global scope
* Function scope
* Block scope
* Module scope

### Example

```javascript
let global = 10;

function test() {
    let local = 20;

    console.log(global); // 10
    console.log(local);  // 20
}
```

---

# 15. What is Lexical Scope?

Lexical scope means a function can access variables based on **where the function was defined**, not where it is called.

```javascript
let name = "Anurag";

function outer() {
    let age = 21;

    function inner() {
        console.log(name);
        console.log(age);
    }

    inner();
}

outer();
```

`inner()` can access variables from its outer lexical environment.

---

# 16. What is a Closure?

A closure occurs when an inner function remembers variables from its outer function even after the outer function has finished execution.

### Example

```javascript
function counter() {
    let count = 0;

    return function() {
        count++;
        return count;
    };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
console.log(increment()); // 3
```

The returned function remembers `count`.

### Interview Answer

> A closure is a function together with its surrounding lexical environment. It allows a function to remember and access variables from its outer scope.

---

# 17. What are Higher-Order Functions?

A higher-order function is a function that:

1. Takes another function as an argument, or
2. Returns another function.

### Example

```javascript
function calculate(a, b, operation) {
    return operation(a, b);
}

const add = (a, b) => a + b;

console.log(calculate(10, 20, add));
```

Here `calculate()` is a higher-order function.

Examples:

```javascript
map()
filter()
reduce()
```

---

# 18. What is a Callback Function?

A callback is a function passed to another function as an argument.

```javascript
function greet(name, callback) {
    console.log("Hello " + name);
    callback();
}

function done() {
    console.log("Done");
}

greet("Anurag", done);
```

Output:

```text
Hello Anurag
Done
```

---

# 19. What is an IIFE?

IIFE means **Immediately Invoked Function Expression**.

It executes immediately after creation.

```javascript
(function() {
    console.log("Executed immediately");
})();
```

Arrow version:

```javascript
(() => {
    console.log("Hello");
})();
```

IIFEs were commonly used to create private scope before modern module systems became common.

---

# 20. What is an Object?

An object stores data in key-value pairs.

```javascript
const user = {
    name: "Anurag",
    age: 21,
    skills: ["JavaScript", "React", "Node"]
};

console.log(user.name);
```

Output:

```text
Anurag
```

---

# 21. Shallow Copy vs Deep Copy

### Shallow Copy

Only the top-level properties are copied.

```javascript
const obj1 = {
    name: "Anurag",
    address: {
        city: "Sonbhadra"
    }
};

const obj2 = { ...obj1 };

obj2.address.city = "Varanasi";

console.log(obj1.address.city);
```

The nested object is still shared.

### Deep Copy

Nested objects are copied as well.

```javascript
const obj2 = structuredClone(obj1);
```

Now changes to nested objects do not affect the original.

---

# 22. How do you clone an object?

### Spread Operator

```javascript
const copy = { ...user };
```

This creates a shallow copy.

### structuredClone

```javascript
const copy = structuredClone(user);
```

This is useful for deep cloning many kinds of structured data.

Another common approach:

```javascript
const copy = JSON.parse(JSON.stringify(user));
```

But this has limitations and should not be treated as a universal deep-cloning solution.

---

# 23. What is Destructuring?

Destructuring allows us to extract values from arrays or objects.

### Object

```javascript
const user = {
    name: "Anurag",
    age: 21
};

const { name, age } = user;

console.log(name);
console.log(age);
```

### Array

```javascript
const numbers = [10, 20, 30];

const [a, b, c] = numbers;

console.log(a); // 10
```

---

# 24. What is the Spread Operator?

The spread operator `...` expands elements of an iterable or properties of an object.

### Array

```javascript
const a = [1, 2];
const b = [3, 4];

const result = [...a, ...b];

console.log(result);
```

Output:

```text
[1, 2, 3, 4]
```

### Object

```javascript
const user = {
    name: "Anurag"
};

const updatedUser = {
    ...user,
    age: 21
};
```

---

# 25. What is the Rest Operator?

The rest operator collects multiple values into an array.

```javascript
function sum(...numbers) {
    return numbers.reduce((total, n) => total + n, 0);
}

console.log(sum(10, 20, 30));
```

Output:

```text
60
```

### Difference

```text
Spread → expands values
Rest   → collects values
```

---

# 26. map vs filter vs reduce

### map()

Transforms every element.

```javascript
const numbers = [1, 2, 3];

const result = numbers.map(n => n * 2);

console.log(result);
// [2, 4, 6]
```

### filter()

Returns elements that satisfy a condition.

```javascript
const result = numbers.filter(n => n > 1);

console.log(result);
// [2, 3]
```

### reduce()

Reduces an array to a single value.

```javascript
const result = numbers.reduce((sum, n) => sum + n, 0);

console.log(result);
// 6
```

---

# 27. forEach vs map

### forEach()

Used to execute something for every element.

```javascript
numbers.forEach(n => {
    console.log(n);
});
```

It does not create a new transformed array.

### map()

Creates and returns a new array.

```javascript
const result = numbers.map(n => n * 2);
```

### Interview Answer

> `forEach()` is generally used for side effects, while `map()` is used when we want to transform an array and receive a new array.

---

# 28. find vs filter

### find()

Returns the **first matching element**.

```javascript
const users = [
    { id: 1, name: "A" },
    { id: 2, name: "B" }
];

const user = users.find(u => u.id === 2);

console.log(user);
```

### filter()

Returns **all matching elements** in an array.

```javascript
const result = users.filter(u => u.id > 0);
```

### Difference

```text
find()   → first matching element
filter() → all matching elements
```

---

# 29. What is Optional Chaining?

Optional chaining `?.` allows us to safely access nested properties.

Without it:

```javascript
console.log(user.address.city);
```

If `address` doesn't exist, an error may occur.

With optional chaining:

```javascript
console.log(user?.address?.city);
```

If something is missing, it returns `undefined` instead of throwing that property-access error.

---

# 30. What is Nullish Coalescing?

The `??` operator provides a default value when the left side is `null` or `undefined`.

```javascript
let name = null;

console.log(name ?? "Guest");
```

Output:

```text
Guest
```

Important difference from `||`:

```javascript
console.log(0 || 100);  // 100
console.log(0 ?? 100);  // 0
```

`??` only treats `null` and `undefined` as missing.

---

# 31. What is the this Keyword?

`this` refers to the object/context associated with the current function invocation.

For a method call:

```javascript
const user = {
    name: "Anurag",

    greet() {
        console.log(this.name);
    }
};

user.greet();
```

Output:

```text
Anurag
```

The exact value of `this` depends on **how a function is called**.

---

# 32. How does this behave in Arrow Functions?

Arrow functions do not create their own `this`.

They inherit `this` from their surrounding lexical scope.

```javascript
const user = {
    name: "Anurag",

    greet: function() {
        const inner = () => {
            console.log(this.name);
        };

        inner();
    }
};

user.greet();
```

Output:

```text
Anurag
```

The arrow function uses the `this` from `greet()`.

---

# 33. What are call(), apply(), and bind()?

These methods allow us to control the `this` value of a function.

### call()

Arguments are passed individually.

```javascript
function greet(city) {
    console.log(this.name, city);
}

const user = {
    name: "Anurag"
};

greet.call(user, "Sonbhadra");
```

### apply()

Arguments are passed as an array.

```javascript
greet.apply(user, ["Sonbhadra"]);
```

### bind()

Returns a new function.

```javascript
const newGreet = greet.bind(user);

newGreet("Sonbhadra");
```

### Difference

```text
call()  → calls immediately, arguments separately
apply() → calls immediately, arguments as array
bind()  → returns a new function
```

---

# 34. What is a Prototype?

Every JavaScript object can have an internal link to another object called its prototype.

The prototype can provide shared properties and methods.

```javascript
const user = {
    name: "Anurag"
};

console.log(Object.getPrototypeOf(user));
```

For ordinary objects, this ultimately links through `Object.prototype`.

---

# 35. What is Prototypal Inheritance?

Objects can inherit properties and methods from other objects through the prototype chain.

```javascript
const animal = {
    eat() {
        console.log("Eating");
    }
};

const dog = Object.create(animal);

dog.bark = function() {
    console.log("Barking");
};

dog.eat();
dog.bark();
```

`dog` can access `eat()` through its prototype.

---

# 36. What is the Prototype Chain?

When JavaScript cannot find a property on an object, it searches its prototype, then the prototype's prototype, and so on.

Example:

```javascript
const user = {
    name: "Anurag"
};

console.log(user.toString());
```

`toString()` is not defined directly on `user`, but JavaScript finds it through the prototype chain.

Conceptually:

```text
user
 ↓
Object.prototype
 ↓
null
```

---

# 37. What are Classes in JavaScript?

Classes provide a cleaner syntax for creating objects and implementing inheritance.

```javascript
class Animal {
    constructor(name) {
        this.name = name;
    }

    sound() {
        console.log("Animal sound");
    }
}

class Dog extends Animal {
    sound() {
        console.log("Bark");
    }
}

const dog = new Dog("Tommy");

dog.sound();
```

Output:

```text
Bark
```

JavaScript classes are built on top of the language's prototype-based inheritance model.

---

# 38. What are Getters and Setters?

Getters and setters allow controlled access to object properties.

```javascript
const user = {
    firstName: "Anurag",
    lastName: "Kumar",

    get fullName() {
        return this.firstName + " " + this.lastName;
    },

    set fullName(value) {
        [this.firstName, this.lastName] = value.split(" ");
    }
};

console.log(user.fullName);

user.fullName = "Rahul Sharma";

console.log(user.fullName);
```

---

# 39. What is Event Bubbling?

Event bubbling means an event starts from the target element and propagates upward through its ancestors.

HTML:

```html
<div id="parent">
    <button id="child">Click</button>
</div>
```

JavaScript:

```javascript
parent.addEventListener("click", () => {
    console.log("Parent");
});

child.addEventListener("click", () => {
    console.log("Child");
});
```

Clicking the button can produce:

```text
Child
Parent
```

The event bubbles from the child to the parent.

---

# 40. What is Event Capturing?

Event capturing is the opposite direction of bubbling.

The event travels from the outer ancestor toward the target.

```javascript
parent.addEventListener(
    "click",
    () => {
        console.log("Parent");
    },
    true
);
```

The third argument `true` enables capture phase handling.

Event flow:

```text
Capturing Phase
      ↓
Target Phase
      ↓
Bubbling Phase
```

---

# 41. Synchronous vs Asynchronous JavaScript

### Synchronous

Tasks execute one after another.

```javascript
console.log("A");
console.log("B");
console.log("C");
```

Output:

```text
A
B
C
```

### Asynchronous

Some operations can complete later without blocking the rest of the JavaScript execution flow.

```javascript
console.log("A");

setTimeout(() => {
    console.log("B");
}, 1000);

console.log("C");
```

Output:

```text
A
C
B
```

---

# 42. What is the Event Loop?

JavaScript uses an event loop to coordinate synchronous execution with asynchronous callbacks.

A simplified model:

```text
Call Stack
    ↓
Web APIs / Runtime APIs
    ↓
Queues
    ↓
Event Loop
    ↓
Call Stack
```

The event loop checks when the call stack is available and then schedules eligible queued callbacks.

---

# 43. What are Call Stack, Web APIs, and Callback Queue?

### Call Stack

Keeps track of currently executing JavaScript functions.

### Web APIs

Browser-provided APIs such as:

```text
setTimeout
DOM events
fetch
```

These are provided by the runtime, not by the JavaScript language itself.

### Callback Queue

Callbacks waiting to be processed can be placed into task queues.

Simplified flow:

```text
JavaScript Code
      ↓
Call Stack
      ↓
Web API
      ↓
Task Queue
      ↓
Event Loop
      ↓
Call Stack
```

**Important:** Promise callbacks use the microtask queue, which has higher priority than the normal task queue.

---

# 44. What is a Promise?

A Promise represents the eventual result of an asynchronous operation.

Example:

```javascript
const promise = new Promise((resolve, reject) => {
    const success = true;

    if (success) {
        resolve("Success");
    } else {
        reject("Failed");
    }
});

promise
    .then(result => console.log(result))
    .catch(error => console.log(error));
```

Promises help manage asynchronous operations.

---

# 45. What are the States of a Promise?

A Promise has three states:

```text
Pending
Fulfilled
Rejected
```

### Pending

Operation is still running.

### Fulfilled

Operation completed successfully.

### Rejected

Operation failed.

Diagram:

```text
             ┌──→ Fulfilled
Pending ─────┤
             └──→ Rejected
```

A settled promise cannot change to another state.

---

# 46. Promise.all(), Promise.allSettled(), Promise.race(), Promise.any()

### Promise.all()

Waits for all promises.

If one rejects, the combined promise rejects.

```javascript
const result = await Promise.all([
    fetchUsers(),
    fetchProducts()
]);
```

### Promise.allSettled()

Waits for all promises regardless of success/failure.

```javascript
const result = await Promise.allSettled([
    fetchUsers(),
    fetchProducts()
]);
```

### Promise.race()

Settles as soon as the first input promise settles.

```javascript
const result = await Promise.race([
    request1(),
    request2()
]);
```

### Promise.any()

Fulfills as soon as the first input promise fulfills.

It rejects only if all input promises reject.

```javascript
const result = await Promise.any([
    request1(),
    request2()
]);
```

### Interview Table

| Method                 | Behavior                |
| ---------------------- | ----------------------- |
| `Promise.all()`        | All must fulfill        |
| `Promise.allSettled()` | Wait for all            |
| `Promise.race()`       | First settled promise   |
| `Promise.any()`        | First fulfilled promise |

---

# 47. What is async/await?

`async/await` provides a cleaner syntax for working with Promises.

### Promise style

```javascript
fetchUser()
    .then(user => {
        console.log(user);
    })
    .catch(error => {
        console.log(error);
    });
```

### async/await

```javascript
async function getUser() {
    try {
        const user = await fetchUser();
        console.log(user);
    } catch (error) {
        console.log(error);
    }
}
```

An `async` function always returns a Promise.

---

# 48. async/await vs then()

Both are based on Promises.

### `.then()`

```javascript
fetchUser()
    .then(user => fetchPosts(user.id))
    .then(posts => console.log(posts))
    .catch(error => console.log(error));
```

### `async/await`

```javascript
async function getData() {
    try {
        const user = await fetchUser();
        const posts = await fetchPosts(user.id);

        console.log(posts);
    } catch (error) {
        console.log(error);
    }
}
```

### Interview Answer

> `async/await` provides syntax that often makes asynchronous code easier to read and reason about, while `.then()` and `.catch()` directly chain Promise handlers.

---

# 49. What is Debouncing vs Throttling?

Both are techniques for controlling how frequently a function executes.

## Debouncing

The function runs after the events stop for a specified amount of time.

Common use:

```text
Search box
```

Example:

```javascript
function debounce(fn, delay) {
    let timer;

    return function(...args) {
        clearTimeout(timer);

        timer = setTimeout(() => {
            fn.apply(this, args);
        }, delay);
    };
}
```

If the user types:

```text
J
Ja
Jav
Java
JavaS
JavaSc
JavaScript
```

The function can execute only after the user stops typing.

## Throttling

The function runs at most once during a specified interval.

Common use:

```text
Scroll events
Mouse movement
Window resize
```

### Difference

```text
Debouncing → wait until activity stops
Throttling → limit execution frequency
```

---

# 50. CommonJS vs ES Modules

Node.js supports CommonJS, while modern JavaScript applications commonly use ES Modules.

## CommonJS

Export:

```javascript
module.exports = add;
```

Import:

```javascript
const add = require("./math");
```

## ES Modules

Export:

```javascript
export default add;
```

Import:

```javascript
import add from "./math.js";
```

### Main Difference

| CommonJS                          | ES Modules                        |
| --------------------------------- | --------------------------------- |
| `require()`                       | `import`                          |
| `module.exports`                  | `export`                          |
| Traditionally common in Node.js   | Standard JavaScript module syntax |
| Usually synchronous loading model | Supports static module structure  |

---

# 🔥 Most Important Questions for MERN Interviews

If you have limited preparation time, prioritize these:

### Must Know

1. `var`, `let`, `const`
2. Hoisting
3. Scope
4. Closure
5. Callback
6. Higher-order functions
7. `this`
8. Arrow functions
9. `call`, `apply`, `bind`
10. Prototype
11. Prototypal inheritance
12. `map`, `filter`, `reduce`
13. Spread and rest
14. Destructuring
15. Shallow vs deep copy
16. Promise
17. `async/await`
18. Event Loop
19. Microtask vs macrotask
20. `Promise.all()`
21. Debouncing
22. Throttling
23. Event bubbling
24. Event capturing
25. CommonJS vs ES Modules

---

# 💻 Important Coding Questions

Along with theory, prepare these JavaScript coding problems:

### 1. Reverse a String

```javascript
function reverse(str) {
    return str.split("").reverse().join("");
}

console.log(reverse("hello"));
```

Output:

```text
olleh
```

---

### 2. Find Maximum Number

```javascript
function maximum(arr) {
    return Math.max(...arr);
}

console.log(maximum([10, 5, 30, 20]));
```

Output:

```text
30
```

---

### 3. Remove Duplicates

```javascript
const numbers = [1, 2, 2, 3, 3, 4];

const unique = [...new Set(numbers)];

console.log(unique);
```

Output:

```text
[1, 2, 3, 4]
```

---

### 4. Count Character Frequency

```javascript
function frequency(str) {
    const result = {};

    for (const char of str) {
        result[char] = (result[char] || 0) + 1;
    }

    return result;
}

console.log(frequency("hello"));
```

Output:

```text
{
    h: 1,
    e: 1,
    l: 2,
    o: 1
}
```

---

### 5. Check Palindrome

```javascript
function isPalindrome(str) {
    return str === str.split("").reverse().join("");
}

console.log(isPalindrome("madam"));
```

Output:

```text
true
```

---

### 6. Find Even Numbers

```javascript
const numbers = [1, 2, 3, 4, 5, 6];

const even = numbers.filter(n => n % 2 === 0);

console.log(even);
```

Output:

```text
[2, 4, 6]
```

---

### 7. Calculate Sum Using reduce()

```javascript
const numbers = [10, 20, 30];

const sum = numbers.reduce((total, n) => total + n, 0);

console.log(sum);
```

Output:

```text
60
```

---

# 🎯 Quick Interview Revision

Remember these one-line definitions:

| Topic         | Short Answer                                       |
| ------------- | -------------------------------------------------- |
| JavaScript    | High-level, dynamically typed programming language |
| Hoisting      | Declarations are processed before execution        |
| Closure       | Function remembers its lexical environment         |
| Callback      | Function passed to another function                |
| HOF           | Function that takes/returns a function             |
| Scope         | Determines where variables are accessible          |
| `this`        | Depends mainly on how a function is called         |
| Promise       | Represents eventual async result                   |
| Event Loop    | Coordinates stack and asynchronous queues          |
| `async/await` | Syntax for working with Promises                   |
| Prototype     | Object used for inheritance/property lookup        |
| `map()`       | Transforms every element                           |
| `filter()`    | Selects matching elements                          |
| `reduce()`    | Reduces values to one result                       |
| Debounce      | Execute after activity stops                       |
| Throttle      | Limit execution frequency                          |
| `===`         | Strict equality                                    |
| `??`          | Default for null/undefined                         |
| Spread        | Expands values                                     |
| Rest          | Collects values                                    |
| IIFE          | Immediately invoked function expression            |

---

# 🚀 MERN Interview Preparation Order

For a MERN Stack interview, study JavaScript in this order:

```text
JavaScript Basics
       ↓
var / let / const
       ↓
Scope + Hoisting
       ↓
Functions
       ↓
Closure
       ↓
Array Methods
       ↓
Objects
       ↓
this
       ↓
Prototype
       ↓
Promises
       ↓
Async/Await
       ↓
Event Loop
       ↓
Microtask / Macrotask
       ↓
Debouncing / Throttling
       ↓
ES Modules
       ↓
React
       ↓
Node.js
       ↓
Express.js
       ↓
MongoDB
```

**Tip:** In an interview, don't only give the definition. Use this structure:

> **Definition → Example → Real-world use case**

For example, for closure:

> "A closure is a function that remembers variables from its outer lexical scope. For example, a counter function can maintain a private count variable. Closures are useful for data privacy, callbacks, and maintaining state."
