# 🚀 Top 30 HTML + CSS Interview Questions & Answers

A collection of the **30 most important HTML and CSS interview questions with simple, interview-ready answers**, especially useful for **Frontend and MERN Stack interviews**.

---

# 📌 HTML Questions

## 1. What is HTML?

**HTML (HyperText Markup Language)** is the standard markup language used to structure content on web pages.

```html
<h1>Hello World</h1>
<p>This is a paragraph.</p>
```

---

## 2. What is HTML5?

HTML5 is the modern version of HTML that introduced new features such as:

* Semantic elements
* Audio and video
* Canvas
* Improved form controls
* Local storage
* Better accessibility

Example:

```html
<header>Header</header>
<main>Main Content</main>
<footer>Footer</footer>
```

---

## 3. What is Semantic HTML?

Semantic HTML uses elements that clearly describe their purpose.

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

we can use:

```html
<header>Header</header>
<main>Content</main>
```

### Benefits

* Better SEO
* Better accessibility
* Better readability
* Easier maintenance

---

## 4. Difference Between `<div>` and `<span>`?

### `<div>`

Generally a block-level element.

```html
<div>Hello</div>
```

### `<span>`

Generally an inline element.

```html
<p>Hello <span>World</span></p>
```

| `<div>`                      | `<span>`                           |
| ---------------------------- | ---------------------------------- |
| Block-level                  | Inline                             |
| Usually starts on a new line | Usually stays in the same line     |
| Used for larger containers   | Used for small portions of content |

---

## 5. Difference Between `id` and `class`?

### ID

Usually used to uniquely identify an element.

```html
<div id="header">
    Header
</div>
```

### Class

Can be applied to multiple elements.

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

### Interview Answer

> An `id` is generally unique, while a `class` can be reused on multiple elements.

---

## 6. What is the purpose of `<!DOCTYPE html>`?

It tells the browser that the document uses HTML5.

```html
<!DOCTYPE html>
```

It also tells the browser to use **standards mode** for rendering the page.

---

## 7. What is the purpose of the `alt` attribute?

The `alt` attribute provides alternative text for an image.

```html
<img
    src="profile.jpg"
    alt="Profile picture">
```

It is useful for:

* Accessibility
* Screen readers
* When an image cannot load
* Describing the image

---

## 8. What is the difference between `<strong>` and `<b>`?

`<b>` makes text visually bold.

```html
<b>Hello</b>
```

`<strong>` indicates that the content has strong importance.

```html
<strong>Warning!</strong>
```

### Interview Answer

> `<b>` is mainly presentational, while `<strong>` provides semantic importance.

---

## 9. What is the difference between `<section>` and `<article>`?

`<section>` represents a thematic section of a page.

```html
<section>
    <h2>Our Services</h2>
</section>
```

`<article>` represents self-contained content.

```html
<article>
    <h2>How to Learn React</h2>
    <p>React is a JavaScript library.</p>
</article>
```

### Simple Answer

> A section groups related content, while an article represents independent, self-contained content.

---

## 10. What is HTML Accessibility?

Accessibility means making websites usable by people with disabilities.

Good practices include:

```html
<img src="logo.png" alt="Company Logo">

<label for="email">Email</label>
<input id="email" type="email">

<button>Submit</button>
```

Important practices:

* Use semantic HTML
* Use meaningful `alt` text
* Use labels for form inputs
* Make interactive elements keyboard accessible

---

# 🎨 CSS Questions

## 11. What is CSS?

**CSS (Cascading Style Sheets)** is used to control the appearance and layout of HTML elements.

Example:

```css
h1 {
    color: blue;
    font-size: 30px;
}
```

HTML:

```html
<h1>Hello World</h1>
```

---

## 12. What are the different ways to apply CSS?

There are three common ways.

### 1. Inline CSS

```html
<p style="color: red;">
    Hello
</p>
```

### 2. Internal CSS

```html
<style>
    p {
        color: red;
    }
</style>
```

### 3. External CSS

```html
<link rel="stylesheet" href="style.css">
```

**External CSS is generally preferred** for maintainability and reuse.

---

## 13. What is the CSS Box Model?

Every HTML element is treated as a box consisting of:

```text
+-------------------------+
|         Margin          |
|  +-------------------+  |
|  |      Border       |  |
|  | +---------------+ |  |
|  | |    Padding    | |  |
|  | | +-----------+ | |  |
|  | | |  Content  | | |  |
|  | | +-----------+ | |  |
|  | +---------------+ |  |
|  +-------------------+  |
+-------------------------+
```

The four parts are:

1. Content
2. Padding
3. Border
4. Margin

Example:

```css
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid black;
    margin: 10px;
}
```

---

## 14. Difference Between `margin` and `padding`?

### Margin

Space **outside** the element's border.

```css
.box {
    margin: 20px;
}
```

### Padding

Space **inside** the element, between content and border.

```css
.box {
    padding: 20px;
}
```

### Easy Trick

> **Margin = Outside**

> **Padding = Inside**

---

## 15. What is `box-sizing: border-box`?

By default:

```css
box-sizing: content-box;
```

The specified width applies only to the content.

With:

```css
* {
    box-sizing: border-box;
}
```

the declared width includes:

* Content
* Padding
* Border

Example:

```css
.box {
    width: 300px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

The total rendered width remains **300px**.

---

## 16. What is CSS Specificity?

Specificity determines which CSS rule wins when multiple rules target the same element.

General order:

```text
Inline styles
    ↓
ID
    ↓
Class / Attribute / Pseudo-class
    ↓
Element / Pseudo-element
```

Example:

```css
p {
    color: blue;
}

.text {
    color: green;
}

#title {
    color: red;
}
```

```html
<p id="title" class="text">
    Hello
</p>
```

The `#title` rule wins because an ID has higher specificity than a class or element selector.

---

## 17. What is Flexbox?

**Flexbox** is a CSS layout system designed mainly for arranging elements in one dimension.

Example:

```css
.container {
    display: flex;
    justify-content: center;
    align-items: center;
}
```

Important properties:

```css
display: flex;
flex-direction:
justify-content:
align-items:
flex-wrap:
gap:
```

---

## 18. Difference Between `justify-content` and `align-items`?

In the default flex direction (`row`):

```css
.container {
    display: flex;
}
```

### `justify-content`

Controls alignment along the **main axis**.

```css
justify-content: center;
```

### `align-items`

Controls alignment along the **cross axis**.

```css
align-items: center;
```

### Easy Trick

> `justify-content` → Main axis

> `align-items` → Cross axis

---

## 19. What is CSS Grid?

CSS Grid is a two-dimensional layout system.

It works with:

* Rows
* Columns

Example:

```css
.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
}
```

This creates three equal columns.

### Flexbox vs Grid

| Flexbox             | Grid                  |
| ------------------- | --------------------- |
| One-dimensional     | Two-dimensional       |
| Row OR column       | Rows AND columns      |
| Good for components | Good for page layouts |

---

## 20. Difference Between `position: relative` and `absolute`?

### Relative

The element remains in the normal document flow but can be visually moved.

```css
.box {
    position: relative;
    top: 20px;
}
```

### Absolute

The element is removed from normal document flow and positioned relative to its nearest positioned ancestor.

```css
.box {
    position: absolute;
    top: 20px;
    right: 10px;
}
```

---

## 21. Difference Between `fixed` and `sticky`?

### Fixed

The element is positioned relative to the viewport.

```css
.navbar {
    position: fixed;
    top: 0;
}
```

It generally remains in the same position while scrolling.

### Sticky

The element behaves like a relatively positioned element until a threshold is reached.

```css
.navbar {
    position: sticky;
    top: 0;
}
```

It then sticks while its scrolling container allows it.

---

## 22. What is `z-index`?

`z-index` controls the stacking order of positioned elements and certain other elements participating in stacking contexts.

```css
.box1 {
    position: relative;
    z-index: 10;
}

.box2 {
    position: relative;
    z-index: 5;
}
```

Generally, the element with the higher applicable stacking order appears above the other.

### Important

`z-index` does not automatically solve every layering issue; stacking contexts can affect the result.

---

## 23. Difference Between `display: none`, `visibility: hidden`, and `opacity: 0`?

### `display: none`

The element is removed from the layout.

```css
.box {
    display: none;
}
```

### `visibility: hidden`

The element is invisible but normally still occupies its layout space.

```css
.box {
    visibility: hidden;
}
```

### `opacity: 0`

The element becomes transparent but normally remains in the layout.

```css
.box {
    opacity: 0;
}
```

It can still receive interaction depending on the element and other CSS.

---

## 24. What is Responsive Web Design?

Responsive design means making a website adapt to different screen sizes.

Common techniques:

* Flexible layouts
* Flexbox
* CSS Grid
* Media queries
* Relative units

Example:

```css
.container {
    width: 80%;
}

@media (max-width: 768px) {
    .container {
        width: 100%;
    }
}
```

---

## 25. What are Media Queries?

Media queries apply CSS based on conditions such as viewport width.

Example:

```css
@media (max-width: 768px) {
    .container {
        flex-direction: column;
    }
}
```

Commonly used for responsive design.

---

## 26. Difference Between `px`, `%`, `em`, and `rem`?

### `px`

Fixed CSS pixel unit.

```css
font-size: 16px;
```

### `%`

Usually relative to a relevant parent/container dimension.

```css
width: 50%;
```

### `em`

Relative to the font size of the relevant element/parent context, depending on the property.

```css
font-size: 2em;
```

### `rem`

Relative to the root element's font size.

```css
font-size: 2rem;
```

### Common Interview Answer

> `rem` is based on the root font size, while `em` is based on the relevant element's font-size context.

---

## 27. What are Pseudo-classes?

Pseudo-classes select elements based on a particular state or condition.

Examples:

```css
button:hover {
    background: black;
}

input:focus {
    border: 2px solid blue;
}

li:first-child {
    color: red;
}
```

Common pseudo-classes:

```text
:hover
:focus
:active
:first-child
:last-child
:nth-child()
```

---

## 28. What are Pseudo-elements?

Pseudo-elements allow you to style a specific part of an element or generate content.

Examples:

```css
p::first-letter {
    font-size: 30px;
}
```

```css
p::before {
    content: "→ ";
}
```

Common pseudo-elements:

```text
::before
::after
::first-letter
::first-line
```

### Difference

> Pseudo-class → element state/condition

> Pseudo-element → part of an element

---

## 29. What is CSS Inheritance?

Inheritance means some CSS properties are passed from a parent element to its descendants.

Example:

```css
body {
    color: blue;
}
```

```html
<body>
    <p>Hello</p>
</body>
```

The paragraph will normally inherit the `color` from `body`.

Not all CSS properties inherit by default.

---

## 30. What are CSS Transitions and Animations?

### Transition

Used to smoothly change a property from one state to another.

```css
button {
    transition: background-color 0.3s;
}

button:hover {
    background-color: black;
}
```

### Animation

Used for more complex or repeated animations.

```css
.box {
    animation: move 2s infinite;
}

@keyframes move {
    from {
        transform: translateX(0);
    }

    to {
        transform: translateX(100px);
    }
}
```

### Difference

> Transition usually happens between two states, while animation can define multiple stages using `@keyframes`.

---

# ⭐ Most Important Questions for MERN Interviews

If you have limited preparation time, prioritize these:

### HTML

* Semantic HTML
* `div` vs `span`
* `id` vs `class`
* Forms
* Accessibility
* `alt`
* HTML5
* `section` vs `article`

### CSS

* Box Model
* `box-sizing`
* Flexbox
* Grid
* `justify-content` vs `align-items`
* `relative` vs `absolute`
* `fixed` vs `sticky`
* `z-index`
* Specificity
* Media Queries
* Responsive Design
* `px` vs `%` vs `em` vs `rem`
* Pseudo-classes
* Pseudo-elements
* `display: none` vs `visibility: hidden`
* Transitions vs Animations

---

# 🎯 Quick Interview Strategy

For every question, try to answer in this format:

```text
1. Definition
2. Why it is used
3. Small example
4. Difference (if applicable)
```

For example:

**Interviewer:** What is Flexbox?

**Good answer:**

> Flexbox is a one-dimensional CSS layout system used to arrange elements in a row or column. It makes alignment and spacing easier. For example, I can use `display: flex`, `justify-content`, and `align-items` to center an element.

This is much better than only saying:

> "Flexbox is used for layout."

---

# 🚀 Next Topics to Prepare

After HTML + CSS, a good **MERN interview preparation order** is:

```text
HTML + CSS
     ↓
JavaScript
     ↓
React
     ↓
Node.js
     ↓
Express.js
     ↓
MongoDB
     ↓
REST API
     ↓
Authentication / JWT
     ↓
Git & GitHub
     ↓
DSA
     ↓
System Design Basics
```

**Target:** Understand the concepts rather than memorizing answers.
