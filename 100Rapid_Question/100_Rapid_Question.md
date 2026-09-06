# ⚛️ React Interview Questions — 100+ Rapid Fire

A rapid-fire collection of React.js interview questions for **MERN Stack Developer interviews**.

> **Practice rule:** Try answering each question yourself in 30–60 seconds before checking your notes.

---

# 🟢 React Basics

1. What is React?
2. Why is React called a library instead of a framework?
3. What are the main features of React?
4. What is a component in React?
5. What is a functional component?
6. What is a class component?
7. Functional component vs class component?
8. What is JSX?
9. Why does React use JSX?
10. Is JSX mandatory in React?
11. What happens to JSX before it reaches the browser?
12. What is `React.createElement()`?
13. What is declarative programming?
14. React vs vanilla JavaScript?
15. What is a Single Page Application?
16. What is Virtual DOM?
17. What is the real DOM?
18. Virtual DOM vs Real DOM?
19. What is reconciliation?
20. What is React Fiber?
21. What is rendering in React?
22. What causes a React component to re-render?
23. Does every re-render cause a DOM update?
24. What is the difference between rendering and committing?
25. What is Strict Mode?
26. Why does React use a component-based architecture?
27. What is component composition?
28. What is a component tree?
29. What is the root of a React application?
30. What is `createRoot()`?

---

# 🟢 JSX

31. What is JSX?
32. JSX vs HTML?
33. Why do we use `className` instead of `class`?
34. Why is `htmlFor` used instead of `for`?
35. Why are JSX attributes usually camelCase?
36. How do you write JavaScript expressions inside JSX?
37. Can you use statements directly inside JSX?
38. How do you conditionally render JSX?
39. How do you render a list in JSX?
40. Why does React require keys when rendering lists?
41. What is a Fragment?
42. Why use `<>...</>`?
43. Can JSX return multiple elements?
44. What is the `children` prop?
45. How do you pass dynamic values to JSX?
46. How do you add inline styles in JSX?
47. How do you add comments inside JSX?
48. Can JSX contain objects directly?
49. What is the difference between `{}` and `{{}}` in JSX?
50. What is a self-closing JSX element?

---

# 🟡 Components

51. What is a reusable component?
52. How do you create a React component?
53. What is component composition?
54. What are props?
55. Can a component modify its props?
56. What is prop drilling?
57. How can you avoid prop drilling?
58. What is the Context API?
59. What is component communication?
60. How does a child communicate with a parent?
61. How can sibling components communicate?
62. What is lifting state up?
63. What are controlled components?
64. What are uncontrolled components?
65. What is a presentational component?
66. What is a container component?
67. What is a Higher-Order Component?
68. What are Render Props?
69. What are Compound Components?
70. What is component composition vs inheritance?

---

# 🟡 Props & State

71. What are props?
72. Are props mutable?
73. What is state?
74. Props vs state?
75. How do you create state in a functional component?
76. What is `useState()`?
77. Why shouldn't state be mutated directly?
78. How do you update an object in state?
79. How do you update an array in state?
80. How do you remove an item from an array in state?
81. How do you update one property of an object state?
82. What is a functional state update?
83. When should you use functional state updates?
84. Why can state appear to be one step behind?
85. What is state batching?
86. Does React batch state updates?
87. Can state be initialized from props?
88. What problems can occur when state is initialized from props?
89. What is derived state?
90. Should derived data always be stored in state?
91. What is lifting state up?
92. What is state ownership?
93. Where should state be stored?
94. When should state become global?
95. What is local state?

---

# 🟡 React Hooks

96. What are Hooks?
97. Why were Hooks introduced?
98. What are the Rules of Hooks?
99. Why can't Hooks be called inside loops?
100. Why can't Hooks be called conditionally?
101. What is `useState()`?
102. What is `useEffect()`?
103. When does `useEffect()` run?
104. What is the dependency array in `useEffect()`?
105. What happens when the dependency array is empty?
106. What happens when there is no dependency array?
107. What is the cleanup function in `useEffect()`?
108. When does an effect cleanup run?
109. How do you clean up an event listener?
110. How do you clean up a timer?
111. How do you fetch API data using `useEffect()`?
112. Why should API requests sometimes be cancelled?
113. What is a stale closure?
114. How can stale closures occur in React?
115. What is `useRef()`?
116. `useRef()` vs `useState()`?
117. How do you access a DOM element using `useRef()`?
118. What is `useContext()`?
119. What is `useReducer()`?
120. `useState()` vs `useReducer()`?
121. What is `useMemo()`?
122. What is `useCallback()`?
123. `useMemo()` vs `useCallback()`?
124. Should you use `useMemo()` everywhere?
125. Should you use `useCallback()` everywhere?
126. What is `useLayoutEffect()`?
127. `useEffect()` vs `useLayoutEffect()`?
128. What is `useId()`?
129. Why shouldn't `useId()` be used as a list key?
130. What is `useTransition()`?
131. What is `useDeferredValue()`?
132. `useTransition()` vs `useDeferredValue()`?
133. What is a Custom Hook?
134. How do you create a Custom Hook?
135. Do Custom Hooks share state?
136. How can you create a `useDebounce()` Hook?
137. How can you create a `useFetch()` Hook?
138. How can you create a `useLocalStorage()` Hook?

---

# 🟡 Events & Forms

139. How are events handled in React?
140. What is a SyntheticEvent?
141. What is event bubbling?
142. What is event capturing?
143. How do you prevent default browser behavior?
144. What does `event.preventDefault()` do?
145. What does `event.stopPropagation()` do?
146. What is the difference between `event.target` and `event.currentTarget`?
147. How do you pass arguments to an event handler?
148. Why is `onClick={handleClick}` different from `onClick={handleClick()}`?
149. How do you handle form submission?
150. What is a controlled input?
151. What is an uncontrolled input?
152. Controlled vs uncontrolled components?
153. How do you handle multiple form fields?
154. How do you handle checkboxes?
155. How do you handle radio buttons?
156. How do you handle a `<select>` element?
157. How do you handle file uploads?
158. How do you validate a form?
159. How do you prevent duplicate form submission?
160. How do you show form validation errors?
161. How do you reset a form?
162. What is `FormData`?
163. How do you upload an image from React to a Node.js backend?
164. How do you handle loading state during form submission?

---

# 🟠 React Router

165. What is React Router?
166. Why is React Router used?
167. What is `BrowserRouter`?
168. What is `Routes`?
169. What is `Route`?
170. What is `Link`?
171. What is `NavLink`?
172. `Link` vs `<a>`?
173. What is `useNavigate()`?
174. When would you use programmatic navigation?
175. What is `useParams()`?
176. What are dynamic routes?
177. What is `useLocation()`?
178. What is `useSearchParams()`?
179. What are query parameters?
180. Route parameters vs query parameters?
181. What are nested routes?
182. What is `Outlet`?
183. What is an index route?
184. How do you create a protected route?
185. How do you implement role-based routing?
186. `Navigate` vs `useNavigate()`?
187. How do you create a 404 page?
188. What is a catch-all route?
189. What is navigation state?
190. How do you implement lazy-loaded routes?

---

# 🟠 API Integration

191. How does React communicate with a backend?
192. What is an API?
193. What is a REST API?
194. What is HTTP?
195. What is JSON?
196. What is the difference between GET and POST?
197. PUT vs PATCH?
198. What is DELETE?
199. How do you make an API request using `fetch()`?
200. How do you make an API request using Axios?
201. Fetch vs Axios?
202. Does `fetch()` automatically reject for HTTP 404 or 500?
203. How do you handle API errors?
204. How do you handle loading state?
205. How do you handle empty API responses?
206. How do you send JSON in a POST request?
207. How do you send FormData?
208. What is an Axios instance?
209. What are Axios interceptors?
210. How do you attach an authentication token to API requests?
211. What is `withCredentials`?
212. How do cookies work with Axios?
213. What is CORS?
214. Why does CORS happen?
215. How do you solve CORS issues?
216. How do you handle a 401 response?
217. How do you handle API timeouts?
218. How do you cancel an API request?
219. How do you prevent duplicate API requests?
220. How do you implement pagination?
221. How do you implement search?
222. Why should search inputs often be debounced?
223. How do you implement filtering?
224. How do you implement sorting?
225. How do you upload images using Cloudinary?
226. Where should API logic be placed in a React project?
227. Why create a centralized API service?
228. Should all API data be stored in Redux?

---

# 🟠 State Management

229. What is state management?
230. When should state be local?
231. When should state be global?
232. What is prop drilling?
233. How does Context solve prop drilling?
234. What is Redux?
235. Why use Redux?
236. What is Redux Toolkit?
237. What is a Redux store?
238. What is an action?
239. What is a reducer?
240. What is dispatch?
241. What is a selector?
242. What is `useSelector()`?
243. What is `useDispatch()`?
244. What is `Provider` in Redux?
245. What is `createSlice()`?
246. What is `configureStore()`?
247. What is Immer?
248. Why can Redux Toolkit code appear to mutate state?
249. What is Redux middleware?
250. What is Redux Thunk?
251. What is `createAsyncThunk()`?
252. How do you handle loading/error/success states in Redux?
253. Redux vs Context?
254. Redux vs Zustand?
255. What is normalized state?
256. What is `createEntityAdapter()`?
257. What should not be stored in Redux?
258. What is derived state?
259. How can Redux cause unnecessary re-renders?
260. How do selectors improve Redux performance?

---

# 🔴 Performance

261. What is React performance optimization?
262. What causes unnecessary re-renders?
263. How can you prevent unnecessary re-renders?
264. What is `React.memo()`?
265. When should you use `React.memo()`?
266. Does `React.memo()` prevent all re-renders?
267. What is memoization?
268. What is referential equality?
269. Why can objects cause unnecessary re-renders?
270. Why can functions cause unnecessary re-renders?
271. How does `useCallback()` help?
272. How does `useMemo()` help?
273. Why shouldn't you memoize everything?
274. What are stable keys?
275. Why shouldn't array indexes usually be used as keys?
276. What is list virtualization?
277. When should you use virtualization?
278. What is pagination?
279. Pagination vs infinite scrolling?
280. What is lazy loading?
281. What is code splitting?
282. What is `React.lazy()`?
283. What is `Suspense`?
284. How does route-based code splitting work?
285. What is tree shaking?
286. How can you reduce bundle size?
287. How can you optimize images?
288. What are Core Web Vitals?
289. What is LCP?
290. What is INP?
291. What is CLS?
292. How can you improve LCP?
293. How can you improve INP?
294. How can you improve CLS?
295. What is debouncing?
296. What is throttling?
297. Debouncing vs throttling?
298. What is the React Profiler?
299. How do you find unnecessary re-renders?
300. How do you optimize a slow React application?

---

# 🔴 Advanced React

301. What is an Error Boundary?
302. What errors can Error Boundaries catch?
303. What errors don't Error Boundaries automatically catch?
304. Why are Error Boundaries traditionally implemented with class components?
305. What is a React Portal?
306. Where are Portals useful?
307. How do events work with Portals?
308. What is `forwardRef()`?
309. What is `useImperativeHandle()`?
310. What is an imperative API?
311. What is a Higher-Order Component?
312. What are Render Props?
313. What are Compound Components?
314. What is component composition?
315. Composition vs inheritance?
316. What is concurrent rendering?
317. What is a transition in React?
318. What is `startTransition()`?
319. What is `useTransition()`?
320. What is `useDeferredValue()`?
321. What is Suspense?
322. What is lazy loading?
323. What is Server-Side Rendering?
324. What is Client-Side Rendering?
325. SSR vs CSR?
326. What is hydration?
327. What is a hydration mismatch?
328. What is streaming SSR?
329. What are React Server Components?
330. Server Components vs Client Components?
331. What is `useSyncExternalStore()`?
332. What is referential equality?
333. What is a stale closure?
334. What are side effects?
335. What is an idempotent effect?
336. Why is cleanup important in effects?
337. How do you prevent memory leaks in React?
338. How do you handle subscriptions in React?
339. How do you integrate WebSockets with React?
340. How do you integrate Socket.IO with React?

---

# 🔴 JavaScript Questions Commonly Asked With React

341. What is a closure?
342. What is lexical scope?
343. What is the event loop?
344. What are microtasks and macrotasks?
345. What is a Promise?
346. Promise vs async/await?
347. What is destructuring?
348. What is the spread operator?
349. What is the rest operator?
350. What is shallow copy?
351. What is deep copy?
352. What is immutability?
353. Why is immutability important in React?
354. What is reference equality?
355. `==` vs `===`?
356. What is optional chaining?
357. What is nullish coalescing?
358. What are higher-order functions?
359. What are `map()`, `filter()`, and `reduce()`?
360. What is debouncing in JavaScript?
361. What is throttling in JavaScript?
362. What is the difference between `let`, `const`, and `var`?
363. What is hoisting?
364. What is `this` in JavaScript?
365. What are arrow functions?
366. Arrow functions vs regular functions?
367. What is a callback?
368. What is callback hell?
369. What is event delegation?
370. What is garbage collection?

---

# 🔥 Scenario-Based React Questions

## 371. Your React component is rendering too many times. How will you debug it?

## 372. Your API is being called twice. What could be the reason?

## 373. Your search API is called on every keystroke. How would you optimize it?

## 374. You have 10,000 products. How would you display them efficiently?

## 375. Your React page takes 5 seconds to load. How would you investigate it?

## 376. A child component renders whenever the parent changes. How would you optimize it?

## 377. You have a large form with 50 fields. How would you improve its performance?

## 378. Your API response contains 10,000 records. Would you store everything in React state?

## 379. Your product images are slowing down the website. What would you do?

## 380. A user types a search query very quickly and old API results overwrite new results. How would you solve it?

## 381. Your Context Provider causes many components to re-render. How would you optimize it?

## 382. Your Redux application has unnecessary re-renders. How would you debug them?

## 383. Your dashboard has multiple expensive charts. How would you optimize it?

## 384. Your application has a huge JavaScript bundle. How would you reduce it?

## 385. How would you implement authentication in a React + Node.js application?

## 386. How would you implement protected routes?

## 387. How would you implement role-based access for Admin, NGO, and Volunteer?

## 388. How would you handle an expired authentication session?

## 389. How would you implement a real-time notification system?

## 390. How would you integrate Socket.IO into React?

---

# 🔥 MERN-Specific React Questions

391. How does React communicate with Express.js?

392. How do you structure a React frontend for a MERN application?

393. Where should API calls be written?

394. How do you handle JWT authentication in React?

395. Where should authentication information be stored?

396. What are the security concerns with storing tokens in localStorage?

397. What are HttpOnly cookies?

398. How does `withCredentials` work?

399. How do you protect frontend routes?

400. Why can't frontend route protection replace backend authorization?

401. How do you handle MongoDB data in React?

402. How do you display paginated MongoDB results?

403. How do you implement product search in MERN?

404. How do you implement filtering in an e-commerce application?

405. How do you implement an image upload using React + Express + Cloudinary?

406. How do you handle API errors from Express in React?

407. How do you display backend validation errors?

408. How do you implement real-time updates using Socket.IO?

409. How would you optimize a MERN e-commerce frontend?

410. How would you optimize a MERN dashboard?

---

# 🧠 Coding Questions

411. Create a counter using `useState()`.

412. Create a Todo application using React.

413. Create a searchable product list.

414. Create a debounced search input.

415. Create a pagination component.

416. Create an infinite scrolling component.

417. Create a reusable Modal component.

418. Create a reusable Button component.

419. Create a reusable Input component.

420. Create a custom `useFetch()` Hook.

421. Create a custom `useDebounce()` Hook.

422. Create a custom `useLocalStorage()` Hook.

423. Create a login form with validation.

424. Create a registration form.

425. Create a password show/hide component.

426. Create a protected route.

427. Create a role-based route.

428. Create a shopping cart using React state.

429. Create a shopping cart using Redux Toolkit.

430. Create a theme switcher using Context API.

431. Create a modal using a Portal.

432. Create a dropdown component.

433. Create an accordion component.

434. Create tabs using Compound Components.

435. Create a reusable API service using Axios.

436. Create an Axios instance with interceptors.

437. Implement API loading/error/success states.

438. Implement image upload using FormData.

439. Implement a product filter.

440. Implement sorting and pagination together.

---

# 💼 Most Important 30 Questions for a MERN Interview

If you have limited time, prepare these first:

1. What is React?
2. What is JSX?
3. Virtual DOM vs Real DOM?
4. What is reconciliation?
5. What are props?
6. What is state?
7. Props vs state?
8. What is `useState()`?
9. What is `useEffect()`?
10. Explain the dependency array.
11. What is `useRef()`?
12. What is Context API?
13. What is prop drilling?
14. What is lifting state up?
15. What is `useMemo()`?
16. What is `useCallback()`?
17. What is `React.memo()`?
18. What causes unnecessary re-renders?
19. What are keys in React?
20. Why shouldn't array indexes usually be used as keys?
21. What is React Router?
22. What is a protected route?
23. How does React communicate with Express?
24. Fetch vs Axios?
25. What is CORS?
26. How does JWT authentication work?
27. Redux vs Context?
28. What is Redux Toolkit?
29. How do you optimize React performance?
30. Explain one of your React/MERN projects in detail.

---

# 🎯 Project-Based Questions

For your own MERN projects, be prepared for questions like:

### Architecture

441. Explain your project architecture.

442. Why did you choose React?

443. Why did you choose Node.js and Express?

444. Why did you choose MongoDB?

445. How does your frontend communicate with your backend?

446. How did you structure your React components?

447. How did you manage application state?

448. Why did you choose Redux/Context/local state?

### Authentication

449. How does login work in your application?

450. How does JWT authentication work?

451. How do you protect routes?

452. How do you implement role-based authorization?

453. What happens when the token/session expires?

### API

454. How many APIs did you create?

455. How did you handle API errors?

456. How did you validate user input?

457. How did you handle loading states?

458. How did you handle duplicate requests?

### Performance

459. What performance problems did you encounter?

460. How did you optimize API latency?

461. How did you optimize images?

462. How did you optimize React rendering?

463. Did you use caching?

464. Did you use pagination?

465. How did you optimize database queries?

### Real-Time

466. Why did you use Socket.IO?

467. How does Socket.IO work in your project?

468. How do you clean up Socket.IO listeners?

469. How do you handle real-time status updates?

---

# 🚀 Rapid Revision Cheat Sheet

```text
React
│
├── JSX
│   └── JavaScript + XML-like syntax
│
├── Components
│   └── Reusable UI
│
├── Props
│   └── Parent → Child data
│
├── State
│   └── Component-managed data
│
├── Hooks
│   ├── useState
│   ├── useEffect
│   ├── useRef
│   ├── useContext
│   ├── useReducer
│   ├── useMemo
│   ├── useCallback
│   ├── useTransition
│   └── Custom Hooks
│
├── Rendering
│   ├── Virtual DOM
│   ├── Reconciliation
│   └── Fiber
│
├── Routing
│   ├── BrowserRouter
│   ├── Routes
│   ├── Route
│   ├── Link
│   ├── useNavigate
│   └── useParams
│
├── State Management
│   ├── Context
│   ├── Redux
│   └── Redux Toolkit
│
├── API
│   ├── Fetch
│   ├── Axios
│   ├── REST
│   ├── CORS
│   └── Authentication
│
├── Performance
│   ├── React.memo
│   ├── useMemo
│   ├── useCallback
│   ├── Lazy Loading
│   ├── Code Splitting
│   ├── Pagination
│   └── Virtualization
│
└── Advanced
    ├── Suspense
    ├── Error Boundaries
    ├── Portals
    ├── SSR
    ├── Hydration
    ├── Streaming
    └── Server Components
```

---

# ⭐ Interview Answer Formula

For technical questions, use this structure:

```text
1. Definition
      ↓
2. Why it is used
      ↓
3. How it works
      ↓
4. Small code example
      ↓
5. Real project use case
      ↓
6. Limitations / when not to use
```

Example:

> **What is useMemo?**

```text
Definition
→ Memoizes a calculated value.

Why?
→ Avoids unnecessary expensive calculations.

How?
→ Recalculates when dependencies change.

Example
→ Filtering a large product list.

Limitation
→ Don't use it for every small calculation.
```

---

# 🔥 Final Preparation Strategy

Before your MERN interview, make sure you can explain without notes:

```text
✅ React Basics
✅ JSX
✅ Components
✅ Props & State
✅ Hooks
✅ useEffect
✅ Context API
✅ Redux Toolkit
✅ React Router
✅ API Integration
✅ Axios
✅ CORS
✅ Authentication
✅ Protected Routes
✅ Performance Optimization
✅ React.memo
✅ useMemo
✅ useCallback
✅ Custom Hooks
✅ Error Boundaries
✅ Suspense
✅ Socket.IO
✅ Your MERN Projects
```

## 🏆 Most Important Rule

> **Don't just memorize React definitions. Be able to explain the concept, write a small example, explain the trade-offs, and connect it to your own MERN project.**
