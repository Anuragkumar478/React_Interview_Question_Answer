# ⚛️ React Router — Interview Questions & Answers

React Router is one of the most important topics for **React and MERN Stack interviews** because most real-world React applications contain multiple pages and authenticated routes.

This file covers:

* Routing basics
* BrowserRouter
* Routes & Route
* Link & NavLink
* useNavigate
* useParams
* useLocation
* Nested Routes
* Dynamic Routes
* Protected Routes
* Layout Routes
* Outlet
* Query Parameters
* Navigation
* 404 Pages
* Authentication Routing
* Lazy Loading
* React Router with MERN

---

## 📚 Table of Contents

1. [What is Routing?](#1-what-is-routing)
2. [What is React Router?](#2-what-is-react-router)
3. [Why Do We Need React Router?](#3-why-do-we-need-react-router)
4. [What is BrowserRouter?](#4-what-is-browserrouter)
5. [What are Routes and Route?](#5-what-are-routes-and-route)
6. [Basic React Router Example](#6-basic-react-router-example)
7. [What is Link?](#7-what-is-link)
8. [Link vs Anchor Tag](#8-link-vs-anchor-tag)
9. [What is NavLink?](#9-what-is-navlink)
10. [Link vs NavLink](#10-link-vs-navlink)
11. [What is useNavigate?](#11-what-is-usenavigate)
12. [How to Navigate Programmatically?](#12-how-to-navigate-programmatically)
13. [What is useParams?](#13-what-is-useparams)
14. [Dynamic Routes](#14-dynamic-routes)
15. [What is useLocation?](#15-what-is-uselocation)
16. [What are Query Parameters?](#16-what-are-query-parameters)
17. [How to Read Query Parameters?](#17-how-to-read-query-parameters)
18. [What are Nested Routes?](#18-what-are-nested-routes)
19. [What is Outlet?](#19-what-is-outlet)
20. [Layout Routes](#20-layout-routes)
21. [Protected Routes](#21-protected-routes)
22. [Authentication with React Router](#22-authentication-with-react-router)
23. [Role-Based Routes](#23-role-based-routes)
24. [What is Navigate?](#24-what-is-navigate)
25. [Navigate vs useNavigate](#25-navigate-vs-usenavigate)
26. [How to Create a 404 Page?](#26-how-to-create-a-404-page)
27. [What is a Catch-All Route?](#27-what-is-a-catch-all-route)
28. [Route Parameters vs Query Parameters](#28-route-parameters-vs-query-parameters)
29. [Optional Parameters](#29-optional-parameters)
30. [Passing State During Navigation](#30-passing-state-during-navigation)
31. [Reading Navigation State](#31-reading-navigation-state)
32. [useSearchParams](#32-usesearchparams)
33. [useMatch](#33-usematch)
34. [Relative Navigation](#34-relative-navigation)
35. [Replace Navigation](#35-replace-navigation)
36. [Back and Forward Navigation](#36-back-and-forward-navigation)
37. [Nested Dynamic Routes](#37-nested-dynamic-routes)
38. [Index Routes](#38-index-routes)
39. [React Router and Browser History](#39-react-router-and-browser-history)
40. [Client-Side Routing](#40-client-side-routing)
41. [SPA vs Traditional Routing](#41-spa-vs-traditional-routing)
42. [Lazy Loading Routes](#42-lazy-loading-routes)
43. [Suspense with Routes](#43-suspense-with-routes)
44. [Route-Level Code Splitting](#44-route-level-code-splitting)
45. [Data Loading in React Router](#45-data-loading-in-react-router)
46. [Navigation and API Requests](#46-navigation-and-api-requests)
47. [React Router in a MERN Application](#47-react-router-in-a-mern-application)
48. [Common Routing Mistakes](#48-common-routing-mistakes)
49. [Most Asked Interview Questions](#49-most-asked-interview-questions)
50. [One-Minute Revision](#50-one-minute-revision)

---

# 1. What is Routing?

Routing determines **which UI should be displayed for a particular URL**.

For example:

```text
/              → Home
/login         → Login
/register      → Register
/products      → Products
/products/123  → Product Details
/cart          → Cart
/profile       → Profile
```

---

# 2. What is React Router?

React Router is a routing library for React applications.

It allows applications to:

* Map URLs to components
* Navigate between pages
* Create nested routes
* Create dynamic routes
* Protect routes
* Read URL parameters
* Manage navigation state

---

# 3. Why Do We Need React Router?

A React SPA can change the displayed UI without performing a full browser page reload.

For example:

```text
Home
  ↓
Products
  ↓
Product Details
```

React Router lets us associate these screens with URLs:

```text
/
 /products
 /products/123
```

This gives users:

* Browser navigation
* Bookmarkable URLs
* Back/forward support
* Deep linking
* Route-based UI

---

# 4. What is BrowserRouter?

`BrowserRouter` provides routing functionality using the browser's History API.

Example:

```jsx
import {
  BrowserRouter
} from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <MyRoutes />
    </BrowserRouter>
  );
}
```

Components using React Router hooks and routing APIs must be inside the router context.

---

# 5. What are Routes and Route?

`Routes` contains route definitions.

`Route` defines a mapping between a URL pattern and an element.

Example:

```jsx
<Routes>
  <Route
    path="/"
    element={<Home />}
  />

  <Route
    path="/about"
    element={<About />}
  />
</Routes>
```

---

# 6. Basic React Router Example

```jsx
import {
  BrowserRouter,
  Routes,
  Route
} from "react-router-dom";

function App() {
  return (
    <BrowserRouter>

      <Routes>

        <Route
          path="/"
          element={<Home />}
        />

        <Route
          path="/about"
          element={<About />}
        />

        <Route
          path="/contact"
          element={<Contact />}
        />

      </Routes>

    </BrowserRouter>
  );
}
```

URL mapping:

```text
/          → Home
/about     → About
/contact   → Contact
```

---

# 7. What is Link?

`Link` is used to navigate between routes without using a normal full-page browser navigation.

Example:

```jsx
import { Link } from "react-router-dom";

<Link to="/products">
  Products
</Link>
```

---

# 8. Link vs Anchor Tag

### Anchor

```html
<a href="/products">
  Products
</a>
```

This normally causes the browser to perform a document navigation.

### React Router Link

```jsx
<Link to="/products">
  Products
</Link>
```

React Router handles the navigation within the SPA.

### Interview Answer

> I use `Link` for internal React Router navigation because it allows client-side navigation without the normal full-page document reload.

---

# 9. What is NavLink?

`NavLink` is similar to `Link`, but it provides information about whether the link matches the current route.

This is useful for navigation menus.

Example:

```jsx
<NavLink to="/products">
  Products
</NavLink>
```

You can use the active state for styling.

```jsx
<NavLink
  to="/products"
  className={({ isActive }) =>
    isActive ? "active" : ""
  }
>
  Products
</NavLink>
```

---

# 10. Link vs NavLink

| Link                         | NavLink                   |
| ---------------------------- | ------------------------- |
| Navigation                   | Navigation                |
| No built-in active-state API | Provides `isActive`       |
| Good for normal links        | Good for navigation menus |

Example:

```text
Footer link → Link

Navbar item → NavLink
```

---

# 11. What is useNavigate?

`useNavigate()` is a React Router hook that allows programmatic navigation.

Example:

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    navigate("/dashboard");
  };

  return (
    <button onClick={handleLogin}>
      Login
    </button>
  );
}
```

---

# 12. How to Navigate Programmatically?

```jsx
const navigate = useNavigate();

navigate("/products");
```

You can also navigate backward:

```jsx
navigate(-1);
```

Forward:

```jsx
navigate(1);
```

And replace the current history entry:

```jsx
navigate("/dashboard", {
  replace: true
});
```

---

# 13. What is useParams?

`useParams()` reads dynamic parameters from the URL.

Suppose:

```jsx
<Route
  path="/products/:id"
  element={<ProductDetails />}
/>
```

URL:

```text
/products/123
```

Then:

```jsx
const { id } = useParams();

console.log(id);
```

Output:

```text
123
```

---

# 14. Dynamic Routes

Dynamic routes contain parameters.

Example:

```jsx
<Route
  path="/users/:userId"
  element={<UserProfile />}
/>
```

URLs:

```text
/users/10
/users/25
/users/100
```

All can render the same component.

Inside the component:

```jsx
const { userId } = useParams();
```

---

# 15. What is useLocation?

`useLocation()` gives information about the current location.

Example:

```jsx
const location = useLocation();

console.log(location.pathname);
console.log(location.search);
console.log(location.state);
```

For:

```text
/products?page=2
```

you might have:

```text
pathname → /products
search   → ?page=2
```

---

# 16. What are Query Parameters?

Query parameters are values placed after `?` in a URL.

Example:

```text
/products?category=books&page=2
```

Here:

```text
category = books
page = 2
```

Query parameters are useful for:

```text
Search
Filtering
Sorting
Pagination
Tabs
```

---

# 17. How to Read Query Parameters?

Using `useSearchParams()`:

```jsx
import {
  useSearchParams
} from "react-router-dom";

function Products() {
  const [searchParams] =
    useSearchParams();

  const category =
    searchParams.get("category");

  const page =
    searchParams.get("page");

  return (
    <div>
      {category} - {page}
    </div>
  );
}
```

For:

```text
/products?category=books&page=2
```

the values are:

```text
books
2
```

---

# 18. What are Nested Routes?

Nested routes allow routes to be structured inside other routes.

Example:

```text
/dashboard
/dashboard/profile
/dashboard/settings
/dashboard/orders
```

Configuration:

```jsx
<Route
  path="/dashboard"
  element={<Dashboard />}
>
  <Route
    path="profile"
    element={<Profile />}
  />

  <Route
    path="settings"
    element={<Settings />}
  />
</Route>
```

---

# 19. What is Outlet?

`Outlet` is used by a parent route to render its matched child route.

Example:

```jsx
function Dashboard() {
  return (
    <div>
      <h1>Dashboard</h1>

      <Outlet />
    </div>
  );
}
```

If the URL is:

```text
/dashboard/profile
```

the `Profile` component renders inside:

```jsx
<Outlet />
```

---

# 20. Layout Routes

A layout route allows multiple routes to share common UI.

Example:

```text
Dashboard
├── Sidebar
├── Navbar
└── Outlet
```

Code:

```jsx
function DashboardLayout() {
  return (
    <>
      <Navbar />
      <Sidebar />

      <main>
        <Outlet />
      </main>
    </>
  );
}
```

Routes:

```jsx
<Route
  path="/dashboard"
  element={<DashboardLayout />}
>
  <Route
    index
    element={<DashboardHome />}
  />

  <Route
    path="users"
    element={<Users />}
  />

  <Route
    path="settings"
    element={<Settings />}
  />
</Route>
```

---

# 21. Protected Routes

A protected route is accessible only when a user satisfies some condition, usually authentication or authorization.

Example:

```jsx
function ProtectedRoute({ children }) {
  const isAuthenticated = true;

  if (!isAuthenticated) {
    return <Navigate to="/login" replace />;
  }

  return children;
}
```

Usage:

```jsx
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

---

# 22. Authentication with React Router

A common MERN flow:

```text
User
 ↓
Login Form
 ↓
Express API
 ↓
Authentication
 ↓
Session/JWT mechanism
 ↓
Frontend user state
 ↓
Protected Route
 ↓
Dashboard
```

Example:

```jsx
function ProtectedRoute({ children }) {
  const { user } = useAuth();

  if (!user) {
    return (
      <Navigate
        to="/login"
        replace
      />
    );
  }

  return children;
}
```

Then:

```jsx
<Route
  path="/dashboard"
  element={
    <ProtectedRoute>
      <Dashboard />
    </ProtectedRoute>
  }
/>
```

---

# 23. Role-Based Routes

Authentication answers:

```text
Is the user logged in?
```

Authorization answers:

```text
Is the user allowed to access this resource?
```

For example:

```text
Admin
NGO
Donor
Volunteer
```

A role-protected component could be:

```jsx
function RoleRoute({
  allowedRoles,
  children
}) {
  const { user } = useAuth();

  if (!user) {
    return <Navigate to="/login" replace />;
  }

  if (!allowedRoles.includes(user.role)) {
    return <Navigate to="/unauthorized" replace />;
  }

  return children;
}
```

Usage:

```jsx
<Route
  path="/admin"
  element={
    <RoleRoute allowedRoles={["admin"]}>
      <AdminDashboard />
    </RoleRoute>
  }
/>
```

---

# 24. What is Navigate?

`Navigate` is a React Router component used to redirect the user.

Example:

```jsx
return (
  <Navigate
    to="/login"
    replace
  />
);
```

Common use cases:

```text
Protected routes
Logout
Unauthorized access
Redirect after form submission
```

---

# 25. Navigate vs useNavigate

### Navigate

Used as a component:

```jsx
<Navigate to="/login" />
```

### useNavigate

Used inside JavaScript logic:

```jsx
const navigate = useNavigate();

navigate("/login");
```

### Easy Rule

```text
Conditional JSX redirect
        ↓
Navigate

Event/function logic
        ↓
useNavigate
```

---

# 26. How to Create a 404 Page?

Use a catch-all route:

```jsx
<Route
  path="*"
  element={<NotFound />}
/>
```

Example:

```jsx
function NotFound() {
  return (
    <h1>
      404 - Page Not Found
    </h1>
  );
}
```

---

# 27. What is a Catch-All Route?

A route using:

```jsx
path="*"
```

can match URLs that don't match the application's more specific routes.

Example:

```jsx
<Routes>

  <Route
    path="/"
    element={<Home />}
  />

  <Route
    path="/products"
    element={<Products />}
  />

  <Route
    path="*"
    element={<NotFound />}
  />

</Routes>
```

---

# 28. Route Parameters vs Query Parameters

### Route Parameter

```text
/products/123
```

Defined as:

```jsx
/products/:id
```

Read using:

```jsx
useParams()
```

### Query Parameter

```text
/products?id=123
```

Read using:

```jsx
useSearchParams()
```

### Typical Usage

```text
/product/123
     ↓
Specific resource

/products?category=books&page=2
     ↓
Filtering/pagination
```

---

# 29. Optional Parameters

React Router versions and route syntax can differ regarding optional route parameters, so don't rely on optional parameters when a clear explicit route structure is simpler.

For example, instead of trying to make one route handle every variation:

```text
/products
/products/:id
```

can often be clearer.

---

# 30. Passing State During Navigation

You can pass navigation state:

```jsx
navigate("/profile", {
  state: {
    from: "dashboard"
  }
});
```

Or with `Link`:

```jsx
<Link
  to="/profile"
  state={{ from: "dashboard" }}
>
  Profile
</Link>
```

This state is intended for navigation-related information and is not a replacement for persistent application state.

---

# 31. Reading Navigation State

Use `useLocation()`:

```jsx
const location = useLocation();

console.log(location.state);
```

For example:

```jsx
const from = location.state?.from;
```

---

# 32. useSearchParams

`useSearchParams()` allows reading and updating URL query parameters.

Example:

```jsx
const [searchParams, setSearchParams] =
  useSearchParams();

const page = searchParams.get("page");
```

Update:

```jsx
setSearchParams({
  page: "2"
});
```

Useful for:

```text
Search
Filters
Sorting
Pagination
```

Example:

```text
/products?search=react&page=2
```

---

# 33. useMatch

`useMatch()` checks whether the current URL matches a particular route pattern.

Example:

```jsx
const match = useMatch("/products/:id");

if (match) {
  console.log(match.params.id);
}
```

It can be useful when a component needs to inspect whether a specific route pattern matches the current location.

---

# 34. Relative Navigation

Nested routes can use relative paths.

Suppose:

```text
/dashboard
/dashboard/settings
```

Inside the dashboard route:

```jsx
<Link to="settings">
  Settings
</Link>
```

This is relative to the current route.

You can also navigate relatively:

```jsx
navigate("../");
```

---

# 35. Replace Navigation

Normally:

```jsx
navigate("/dashboard");
```

adds a new entry to browser history.

With:

```jsx
navigate("/dashboard", {
  replace: true
});
```

the current history entry is replaced.

This is useful after operations such as:

```text
Login
Logout
Redirect after temporary pages
```

For example:

```jsx
navigate("/dashboard", {
  replace: true
});
```

prevents the login page from remaining as the previous history entry in that navigation flow.

---

# 36. Back and Forward Navigation

Go back:

```jsx
navigate(-1);
```

Go forward:

```jsx
navigate(1);
```

This uses browser history navigation.

---

# 37. Nested Dynamic Routes

You can combine nesting and dynamic parameters.

Example:

```text
/dashboard/users/123
```

Routes:

```jsx
<Route
  path="/dashboard"
  element={<Dashboard />}
>
  <Route
    path="users/:id"
    element={<UserProfile />}
  />
</Route>
```

Inside `UserProfile`:

```jsx
const { id } = useParams();
```

---

# 38. Index Routes

An index route renders the default child route of a parent.

Example:

```jsx
<Route
  path="/dashboard"
  element={<Dashboard />}
>
  <Route
    index
    element={<DashboardHome />}
  />

  <Route
    path="settings"
    element={<Settings />}
  />
</Route>
```

So:

```text
/dashboard
```

renders:

```text
DashboardHome
```

while:

```text
/dashboard/settings
```

renders:

```text
Settings
```

---

# 39. React Router and Browser History

React Router works with browser navigation mechanisms so URLs can change without requiring a full document reload for normal client-side navigation.

This allows:

```text
Back
Forward
Refresh
Bookmarks
Direct URLs
```

to work with application routing, provided the deployment server is configured correctly.

---

# 40. Client-Side Routing

In client-side routing:

```text
URL changes
      ↓
React Router matches route
      ↓
React renders component
```

The browser does not need to download a completely new HTML document for every internal navigation.

This is a key feature of SPAs.

---

# 41. SPA vs Traditional Routing

### Traditional routing

```text
Request /products
       ↓
Server
       ↓
HTML response
       ↓
Browser loads page
```

### SPA routing

```text
React Application
       ↓
URL changes
       ↓
Router matches route
       ↓
Component changes
```

However, the backend/server still needs to correctly serve the SPA entry point for direct navigation to client-side routes.

---

# 42. Lazy Loading Routes

Routes can be lazy-loaded to reduce the initial JavaScript bundle.

Example:

```jsx
import { lazy } from "react";

const Dashboard = lazy(
  () => import("./pages/Dashboard")
);
```

Then:

```jsx
<Route
  path="/dashboard"
  element={<Dashboard />}
/>
```

Usually this is combined with `Suspense`.

---

# 43. Suspense with Routes

```jsx
<Suspense fallback={<p>Loading...</p>}>
  <Routes>
    <Route
      path="/dashboard"
      element={<Dashboard />}
    />
  </Routes>
</Suspense>
```

When the lazy component is loading:

```text
Loading...
```

is displayed.

---

# 44. Route-Level Code Splitting

Instead of loading every page's JavaScript immediately:

```text
Home
Products
Dashboard
Admin
Reports
Settings
```

you can load some pages only when needed.

Example:

```text
Initial bundle
      ↓
Home

User opens Dashboard
      ↓
Dashboard chunk loads
```

Benefits:

* Smaller initial bundle
* Faster initial loading
* Better scalability for large applications

---

# 45. Data Loading in React Router

Modern React Router also supports route-level data APIs depending on the router setup.

Conceptually:

```text
Route
 ↓
Loader
 ↓
Fetch data
 ↓
Route component
```

This can allow routing and data loading to be coordinated.

For simpler applications, fetching with component logic or a dedicated data-fetching layer may also be appropriate.

---

# 46. Navigation and API Requests

A common MERN flow:

```text
Product Page
     ↓
POST /api/cart
     ↓
Success
     ↓
navigate("/cart")
```

Example:

```jsx
const handleAddToCart = async () => {
  await axios.post(
    "/api/cart",
    { productId }
  );

  navigate("/cart");
};
```

You should generally navigate **after** the required API operation succeeds.

---

# 47. React Router in a MERN Application

A typical MERN application might have:

```text
/
├── /login
├── /register
├── /products
├── /products/:id
├── /cart
├── /checkout
├── /profile
└── /admin
```

Architecture:

```text
                    React
                      │
                React Router
                      │
        ┌─────────────┼─────────────┐
        ↓             ↓             ↓
      Public       Protected      Admin
      Routes         Routes        Routes
        │              │             │
        └──────────────┼─────────────┘
                       ↓
                    Axios
                       ↓
                  Express API
                       ↓
                    MongoDB
```

---

# 48. Common Routing Mistakes

## Mistake 1 — Using `<a>` for internal routes

Instead of:

```jsx
<a href="/products">
  Products
</a>
```

prefer:

```jsx
<Link to="/products">
  Products
</Link>
```

for normal internal React Router navigation.

---

## Mistake 2 — Forgetting `Outlet`

If you define nested routes but don't render:

```jsx
<Outlet />
```

the child route's UI has nowhere to appear in the parent layout.

---

## Mistake 3 — Protecting Only the Frontend

A frontend protected route improves UX, but it is **not a security boundary**.

The backend must also verify:

```text
Authentication
Authorization
Permissions
```

for protected API operations.

---

## Mistake 4 — Putting Everything in Query Parameters

Don't use query parameters for every piece of state.

Use them when the value naturally belongs in the URL:

```text
search
filter
sort
page
```

---

## Mistake 5 — Putting Sensitive Data in URLs

URLs can appear in:

```text
Browser history
Logs
Analytics
Referrer-related systems
```

Therefore, don't put sensitive secrets or credentials into route/query parameters.

---

## Mistake 6 — Forgetting Deployment Configuration

A React SPA may work locally but return a server 404 when directly opening:

```text
/dashboard
```

on production.

The hosting server must be configured to serve the application's entry HTML for appropriate client-side routes.

---

# 49. Most Asked Interview Questions

### Basic

1. What is routing?
2. What is React Router?
3. Why do we need React Router?
4. What is `BrowserRouter`?
5. What are `Routes` and `Route`?
6. What is `Link`?
7. What is `NavLink`?
8. Link vs NavLink?
9. Link vs `<a>`?
10. What is `useNavigate()`?

### Parameters

11. What is `useParams()`?
12. What are dynamic routes?
13. What are query parameters?
14. What is `useSearchParams()`?
15. Route parameters vs query parameters?
16. What is `useLocation()`?

### Nested Routing

17. What are nested routes?
18. What is `Outlet`?
19. What are layout routes?
20. What are index routes?
21. What are relative routes?

### Authentication

22. What is a protected route?
23. How do you implement protected routes?
24. How do you implement role-based routing?
25. `Navigate` vs `useNavigate()`?
26. How do you redirect after login?
27. Why is frontend route protection not enough for security?

### Advanced

28. What is lazy loading?
29. Why use route-level code splitting?
30. How does `Suspense` work with lazy routes?
31. What is a 404/catch-all route?
32. How does React Router use browser history?
33. What happens when a user directly opens a nested SPA URL?
34. How do you handle routing in a MERN application?

---

# 50. One-Minute Revision

Remember these:

```text
BrowserRouter
     ↓
Provides router context

Routes
     ↓
Contains route definitions

Route
     ↓
Maps URL → UI

Link
     ↓
Client-side navigation

NavLink
     ↓
Link + active state

useNavigate
     ↓
Programmatic navigation

useParams
     ↓
Read dynamic URL parameters

useLocation
     ↓
Read current location

useSearchParams
     ↓
Read/update query parameters

Outlet
     ↓
Render nested route

Navigate
     ↓
Redirect

path="*"
     ↓
404 / catch-all

lazy + Suspense
     ↓
Route code splitting
```

---

# 🎯 React Router Interview Formula

When asked:

> How would you structure routing in a MERN application?

A strong answer:

> I would divide the application into public, protected, and role-based routes. I would use React Router for client-side navigation, `BrowserRouter` with route definitions, `Link` or `NavLink` for navigation, and `useNavigate` for programmatic redirects. Dynamic resources such as `/products/:id` would use `useParams`, while search and filtering could use query parameters. For authenticated pages I would use protected route components, but I would also enforce authentication and authorization on the Express backend because frontend route protection alone is not a security mechanism. For larger applications, I would use nested layouts, `Outlet`, and lazy-loaded routes where appropriate.

---

# 🚀 MERN Example

For an NGO platform, routing could look like:

```text
/
│
├── /login
├── /register
├── /campaigns
├── /campaigns/:id
│
├── /dashboard
│   ├── /dashboard/profile
│   ├── /dashboard/donations
│   └── /dashboard/campaigns
│
└── /admin
    ├── /admin/users
    └── /admin/verification
```

The routing architecture could be:

```text
                 App
                  │
            React Router
                  │
        ┌─────────┼─────────┐
        ↓         ↓         ↓
      Public   Protected    Admin
      Routes     Routes     Routes
                  │
                  ↓
            Authentication
                  │
                  ↓
             Authorization
                  │
                  ↓
             Express API
                  │
                  ↓
              MongoDB
```

This structure keeps routing, authentication, authorization, and backend security responsibilities clearly separated.

---

# 🔥 Top 10 Questions to Prepare First

If your interview is tomorrow, prepare these first:

```text
1. What is React Router?

2. BrowserRouter vs Routes vs Route?

3. Link vs NavLink?

4. Link vs <a>?

5. useNavigate() vs Navigate?

6. What is useParams()?

7. What are nested routes?

8. What is Outlet?

9. How do you implement protected routes?

10. How would you implement routing in a MERN application?
```

These questions cover a large portion of the React Router concepts commonly discussed in React/MERN interviews.
