# 🚀 Top 30 HTML Interview Questions & Answers

A collection of the **30 most important HTML interview questions with simple, interview-ready answers**, especially useful for **Frontend and MERN Stack interviews**.

---

## 1. What is HTML?

**HTML (HyperText Markup Language)** is the standard markup language used to create and structure content on web pages.

```html
<h1>Hello World</h1>
<p>This is a paragraph.</p>
```

---

## 2. What is HTML5?

**HTML5** is the modern version of HTML that introduced many new features such as:

* Semantic elements
* Audio and video
* Canvas
* Improved forms
* Local storage
* Better accessibility

Example:

```html
<header>Website Header</header>
<main>Main Content</main>
<footer>Website Footer</footer>
```

---

## 3. What is an HTML Element?

An HTML element usually consists of an opening tag, content, and closing tag.

```html
<p>Hello World</p>
```

Here:

* `<p>` → Opening tag
* `Hello World` → Content
* `</p>` → Closing tag

Some elements are **void elements** and don't have closing tags:

```html
<img src="image.jpg">
<br>
<input type="text">
```

---

## 4. What are HTML Attributes?

Attributes provide additional information about an HTML element.

```html
<a href="https://example.com" target="_blank">
    Visit Website
</a>
```

Here:

* `href` → Attribute
* `target` → Attribute

---

## 5. Difference Between `<div>` and `<span>`?

### `<div>`

`div` is generally a **block-level** container.

```html
<div>Hello</div>
```

### `<span>`

`span` is generally an **inline** container.

```html
<p>Hello <span>World</span></p>
```

### Main Difference

| `<div>`                  | `<span>`                           |
| ------------------------ | ---------------------------------- |
| Block-level              | Inline                             |
| Starts on a new line     | Doesn't normally start a new line  |
| Used for larger sections | Used for small portions of content |

---

## 6. What is Semantic HTML?

Semantic HTML uses elements that clearly describe their meaning.

Examples:

```html
<header>
<nav>
<main>
<section>
<article>
<aside>
<footer>
```

Instead of:

```html
<div>Header</div>
<div>Content</div>
```

we can write:

```html
<header>Header</header>
<main>Content</main>
```

### Benefits

* Better SEO
* Better accessibility
* Better code readability
* Easier maintenance

---

## 7. Difference Between Block and Inline Elements?

### Block Elements

Generally start on a new line and take the available width.

Examples:

```html
<div>
<p>
<h1>
<section>
```

### Inline Elements

Generally take only the required width.

Examples:

```html
<span>
<a>
<strong>
<em>
```

---

## 8. What is `<!DOCTYPE html>`?

`<!DOCTYPE html>` tells the browser that the document is an **HTML5 document**.

```html
<!DOCTYPE html>
```

It also makes the browser use **standards mode** for rendering.

---

## 9. What is the `<head>` Tag?

The `<head>` contains metadata and resources related to the webpage.

Example:

```html
<head>
    <title>My Website</title>

    <meta charset="UTF-8">

    <meta name="description"
          content="My Website">

    <link rel="stylesheet"
          href="style.css">
</head>
```

---

## 10. Difference Between `<head>` and `<header>`?

### `<head>`

Contains metadata and resources.

```html
<head>
    <title>My Website</title>
</head>
```

### `<header>`

Represents visible introductory content.

```html
<header>
    <h1>My Website</h1>
</header>
```

**Simple answer:**

> `<head>` is for document information, while `<header>` is for visible page/section content.

---

## 11. What is the `<meta>` Tag?

The `<meta>` tag provides metadata about the webpage.

Example:

```html
<meta charset="UTF-8">
```

For responsive websites:

```html
<meta name="viewport"
      content="width=device-width, initial-scale=1.0">
```

The viewport tag helps webpages display properly on different screen sizes.

---

## 12. Difference Between `id` and `class`?

### ID

Used to uniquely identify an element.

```html
<div id="header">
    Header
</div>
```

### Class

Can be used on multiple elements.

```html
<p class="text">Hello</p>
<p class="text">World</p>
```

CSS:

```css
#header {
    color: red;
}

.text {
    color: blue;
}
```

### Simple Difference

> `id` is generally unique, while a `class` can be reused.

---

## 13. Difference Between `<strong>` and `<b>`?

`<b>` makes text visually bold.

```html
<b>Hello</b>
```

`<strong>` indicates that the content has **strong importance**.

```html
<strong>Warning!</strong>
```

### Interview Answer

> `<b>` is mainly presentational, while `<strong>` has semantic meaning.

---

## 14. Difference Between `<em>` and `<i>`?

`<i>` represents text in an alternate voice or style.

```html
<i>Hello</i>
```

`<em>` represents emphasized text.

```html
<em>Important</em>
```

### Interview Answer

> `<em>` has semantic meaning for emphasis, while `<i>` represents text in an alternate voice or style.

---

## 15. What is the `<form>` Element?

The `<form>` element is used to collect user input.

Example:

```html
<form>
    <input type="text">

    <input type="email">

    <button type="submit">
        Submit
    </button>
</form>
```

Forms are commonly used for:

* Login
* Registration
* Search
* Contact forms
* Payments

---

## 16. What are Common HTML Input Types?

Common input types include:

```html
<input type="text">

<input type="email">

<input type="password">

<input type="number">

<input type="date">

<input type="file">

<input type="checkbox">

<input type="radio">

<input type="submit">
```

---

## 17. Difference Between GET and POST?

### GET

Sends data as part of the URL.

```html
<form method="GET">
```

Example:

```text
/search?query=phone
```

Commonly used for retrieving/searching data.

### POST

Sends data in the request body.

```html
<form method="POST">
```

Commonly used when submitting data to a server.

### Simple Interview Answer

> GET is commonly used to retrieve data, while POST is commonly used to submit data.

---

## 18. What is the Purpose of `<label>`?

`<label>` provides a description for a form input and associates the text with that input.

```html
<label for="email">
    Email
</label>

<input
    id="email"
    type="email">
```

Clicking the label can focus the input.

### Benefits

* Better accessibility
* Better user experience
* Screen-reader friendly

---

## 19. Difference Between `<button>` and `<input type="submit">`?

Both can submit forms.

```html
<input type="submit" value="Submit">
```

or:

```html
<button type="submit">
    Submit
</button>
```

`<button>` is more flexible because it can contain HTML content.

```html
<button type="submit">
    <strong>Submit</strong>
</button>
```

---

## 20. What is the Purpose of the `alt` Attribute?

The `alt` attribute provides alternative text for an image.

```html
<img
    src="cat.jpg"
    alt="White cat sitting on a chair">
```

It helps with:

* Accessibility
* Screen readers
* When an image fails to load
* Understanding image content

---

## 21. Difference Between `<a>` and `<link>`?

### `<a>`

Creates a clickable hyperlink.

```html
<a href="/about">
    About Us
</a>
```

### `<link>`

Connects the current document to an external resource.

```html
<link
    rel="stylesheet"
    href="style.css">
```

### Simple Answer

> `<a>` is used for navigation, while `<link>` is used to connect external resources.

---

## 22. Difference Between `<section>` and `<article>`?

### `<section>`

Represents a thematic section of a webpage.

```html
<section>
    <h2>Our Services</h2>
    <p>We provide web development services.</p>
</section>
```

### `<article>`

Represents self-contained content.

```html
<article>
    <h2>How to Learn React</h2>
    <p>React is a JavaScript library...</p>
</article>
```

### Simple Answer

> A section groups related content, while an article represents independent, self-contained content.

---

## 23. What is an `<iframe>`?

An `<iframe>` embeds another webpage or external content inside the current webpage.

Example:

```html
<iframe
    src="https://example.com"
    title="Example Website">
</iframe>
```

It can be used for:

* Maps
* Videos
* External pages
* Embedded documents

---

## 24. What is HTML Accessibility?

Accessibility means making websites usable by people with disabilities.

Good practices include:

### Use semantic HTML

```html
<nav>
    ...
</nav>
```

### Use `alt` for meaningful images

```html
<img src="logo.png"
     alt="Company Logo">
```

### Associate labels with inputs

```html
<label for="name">
    Name
</label>

<input id="name">
```

### Use buttons for actions

```html
<button>
    Submit
</button>
```

---

## 25. What are HTML Entities?

HTML entities are special codes used to represent reserved or special characters.

Examples:

```text
&lt;    → <
&gt;    → >
&amp;   → &
&nbsp;  → Non-breaking space
```

Example:

```html
<p>5 &lt; 10</p>
```

Output:

```text
5 < 10
```

---

## 26. Difference Between `<ul>`, `<ol>` and `<dl>`?

### `<ul>` — Unordered List

```html
<ul>
    <li>Apple</li>
    <li>Banana</li>
</ul>
```

### `<ol>` — Ordered List

```html
<ol>
    <li>Login</li>
    <li>Checkout</li>
</ol>
```

### `<dl>` — Description List

```html
<dl>
    <dt>HTML</dt>
    <dd>Markup language used to structure webpages.</dd>
</dl>
```

---

## 27. Difference Between localStorage, sessionStorage and Cookies?

| Feature                | localStorage           | sessionStorage         | Cookies                |
| ---------------------- | ---------------------- | ---------------------- | ---------------------- |
| Lifetime               | Until cleared          | Until session/tab ends | Configurable           |
| Capacity               | Larger                 | Larger                 | Small                  |
| Sent with HTTP request | No                     | No                     | Yes                    |
| JavaScript access      | Yes                    | Yes                    | Yes, unless `HttpOnly` |
| Common use             | Persistent client data | Temporary data         | Sessions/auth          |

Example:

```javascript
localStorage.setItem("name", "Anurag");
```

---

## 28. Difference Between `async` and `defer`?

Normal script:

```html
<script src="app.js"></script>
```

The browser can pause HTML parsing while the script is fetched and executed.

### async

```html
<script
    async
    src="app.js">
</script>
```

The script downloads without blocking HTML parsing and executes as soon as it is ready.

### defer

```html
<script
    defer
    src="app.js">
</script>
```

The script downloads while HTML parsing continues and executes after the document has been parsed.

### Important Difference

> `async` executes as soon as the script is ready, while `defer` executes after HTML parsing and maintains the order of deferred scripts.

---

## 29. What is the Difference Between `<canvas>` and `<svg>`?

### Canvas

Used for drawing graphics using JavaScript.

```html
<canvas id="myCanvas">
</canvas>
```

Canvas is **pixel-based**.

### SVG

Used for vector graphics.

```html
<svg width="100" height="100">
    <circle
        cx="50"
        cy="50"
        r="40">
    </circle>
</svg>
```

SVG graphics can scale without losing quality.

### Simple Answer

> Canvas is raster/pixel-based drawing, while SVG is vector-based graphics.

---

## 30. What is the Difference Between `display: none` and the HTML `hidden` Attribute?

`display: none` is a **CSS property**:

```html
<div style="display: none;">
    Hello
</div>
```

The element is not displayed.

HTML also provides the `hidden` attribute:

```html
<div hidden>
    Hello
</div>
```

The browser normally renders a hidden element as not displayed.

### Simple Interview Answer

> Both can hide an element visually, but `hidden` is an HTML semantic state, while `display: none` is a CSS presentation rule.

---

# ⭐ Most Important Questions for MERN Interviews

If you have limited preparation time, focus especially on:

1. **HTML vs HTML5**
2. **Semantic HTML**
3. **Block vs Inline**
4. **`div` vs `span`**
5. **`id` vs `class`**
6. **GET vs POST**
7. **Forms and input types**
8. **`alt` attribute**
9. **Accessibility**
10. **localStorage vs sessionStorage vs cookies**
11. **`async` vs `defer`**
12. **`section` vs `article`**
13. **`strong` vs `b`**
14. **`head` vs `header`**
15. **Canvas vs SVG**

> **Interview tip:** Don't just memorize the definitions. For each question, understand **what it is, why it is used, and give a small code example**. This makes your answer much stronger in a technical interview.
