                 React Performance Based Questions

1. General Performance Optimization
How does React's reconciliation process work, and how can you optimize it ?
Ans -> React's reconciliation process involves comparing a virtual DOM representation of your UI with the previous version to determine what changes need to be applied to the actual DOM. Here's how it works and how you can optimize it :-
React Reconciliation Process
Virtual DOM Creation: When state changes, React creates a new virtual DOM tree.
Diffing Algorithm: React compares the new virtual DOM with the previous one, identifying differences (the "diff").
Component Updates: React determines which components need to re-render based on:
Changed props or state
Parent re-renders
Reconciliation: Changes are batched and applied efficiently to the real DOM.
Real DOM: Not just a JavaScript representation; it’s the actual DOM structure of HTML elements.
Virtual DOM: JavaScript representation of DOM elements and properties.
What are the best ways to prevent unnecessary re-renders in React?
Ans ->
                     Optimization
Use Case
React.memo
Prevents re-renders when props remain the same
useCallback
Prevents function re-creation
useMemo
Avoids expensive recalculations
Splitting Components
Isolates frequently and rarely changing states
Avoiding Unnecessary State Updates
Prevents redundant renders
Optimizing Context API
Reduces unnecessary consumer re-renders
Using Immutable Data
Ensures state updates trigger re-renders
Using Proper Keys in Lists
Avoids unnecessary re-renders in lists


How does React handle updates, and how can you optimize them for performance?


What is the Virtual DOM, and how does it improve performance?
Ans -> The Virtual DOM (VDOM) is a lightweight copy of the real DOM that React uses to optimize UI updates. Instead of updating the actual DOM directly (which is slow), React updates the Virtual DOM first, calculates the changes (diffing), and applies only the necessary updates to the real DOM.
How does React batch state updates, and when does it not batch them ?
Ans -> React automatically batches multiple state updates into a single render to improve performance. This means that when you call setState multiple times in a single event handler, React groups them and re-renders the component only once, instead of re-rendering after each update.
>>>> React does not batch state updates when they occur inside native event listeners, Promises, setTimeout, or async functions (outside React’s synthetic event system).
🎯 Key Takeaways
React batches state updates inside event handlers to avoid unnecessary re-renders.


In older React versions (≤17), updates in async functions (setTimeout, Promises) are not batched.


React 18 automatically batches updates in async functions, improving performance.


Use flushSync if you need updates to be applied immediately.
Example of Flush Sync -> 
const addBox = () => {
   flushSync(() => {
     setBoxes(prev => [...prev, {}]);
   });
  const height = containerRef.current.offsetHeight;
  console.log("Height after update:", height);
};

      				  React Fiber https://sunnychopper.medium.com/what-is-react-fiber-and-how-it-helps-you-build-a-high-performing-react-applications-57bceb706ff3
React Fiber is the core architectural rewrite of the React reconciliation engine introduced in React 16. It changed React from a synchronous, stack-based system to an asynchronous, incremental one, enabling features like Concurrent Mode and Suspense. 
Key Concepts
Incremental Rendering: React Fiber breaks large rendering tasks into smaller "units of work" (fibers). This allows the engine to pause, resume, or even abort work to ensure the main thread remains responsive for urgent tasks like user input.
Scheduling & Prioritization: Tasks are assigned different priority levels. High-priority updates (e.g., animations, keystrokes) are handled immediately via requestAnimationFrame, while lower-priority work (e.g., loading data for a list) is deferred to idle periods using requestIdleCallback.
Fiber Node Structure: A "fiber" is a plain JavaScript object representing a unit of work for a specific component. Unlike the old recursive stack, fibers are linked together (via child, sibling, and return pointers), effectively creating a virtual stack frame that can be managed manually. 
The Two Rendering Phases
Render/Reconciliation Phase (Asynchronous): React builds a "work-in-progress" tree to determine what changes are needed. This phase can be interrupted or paused if more important tasks arise because it makes no changes to the actual DOM.
Commit Phase (Synchronous): Once the work is complete, React applies all calculated changes to the DOM in a single pass. This phase is never interrupted to avoid showing a partially updated or inconsistent UI. 
Common Confusions
Fiber vs. React Three Fiber (R3F): While they share the name, React Three Fiber is specifically a React renderer for Three.js, allowing you to build 3D scenes declaratively.
Fiber vs. Virtual DOM: The Virtual DOM is a general programming concept for keeping a UI representation in memory. Fiber is the specific engine that performs the diffing (reconciliation) and scheduling within that concept.
2. React Hooks & State Management
What are some ways to optimize performance when using useState?
Ans -> 
      🔥 Optimization
                    ✅ Best Practice
Use Functional Updates
      setState((prev) => prev + 1);
Lazy Initialization
      useState(() => expensiveComputation());
Avoid Unnecessary Updates
setState((prev) => prev === newValue ? prev : newValue);
Use useReducer for Complex State
Instead of multiple useState calls
Avoid Derived State
Compute derived values inside render
Batch Updates
React 18+ does this automatically
Use useCallback for Handlers
Prevent unnecessary function re-creations
Flatten Complex State
Use multiple useState instead of deeply nested objects

🔄 Lazy Initialization in React (useState(() => ...))
✅ What is Lazy Initialization?
Lazy initialization is a performance optimization technique where initial state computation is deferred until the component is mounted. Instead of computing the initial value every time the component renders, React will only compute it once—on the first render.

💡 React Example:
const [value, setValue] = useState(() => expensiveComputation());
🧠 What Happens Here ?
expensiveComputation() is not immediately executed.


Instead, the function () => expensiveComputation() is passed to React, and React calls it only once during the first render to initialize the state.


On subsequent re-renders, expensiveComputation() is not called again.



🚫 Without Lazy Initialization:
const [value, setValue] = useState(expensiveComputation());

In this case, expensiveComputation() runs every time the component renders—even if it's not needed—which can lead to performance issues.

⚙️ When Should You Use It ?
When computing the initial state is expensive (e.g., parsing large data, filtering arrays, etc.) .


To optimize performance and avoid unnecessary computations on every render.

✅ Final Tip
Use lazy initialization only when the initial state is expensive to calculate. For simple values, it's not necessary and may add unnecessary complexity.

How can you use useMemo and useCallback to improve React performance?


What are the performance implications of using Context API, and how can you optimize it ?
Ans -> 
How Context API Causes Performance Issues
Every Context Consumer Re-renders When the Value Changes


Even if a small part of the context changes, all consuming components will re-render.


Re-renders Cascade Down the Component Tree


If a parent component using context re-renders, all child components also re-render.
Frequent Context Value Updates Can Slow Down UI


If the context is updated often (e.g., for real-time data), components may re-render unnecessarily.
	CODEWISE EXAMPLE
-> Great! Let's talk about real-world rendering problems in React when using useContext — especially around performance, unnecessary re-renders, and stale values.

🚨 Problem: Unnecessary Re-renders with useContext
🧠 Why it happens:
Whenever a context value changes, all components consuming that context re-render, even if the component only uses part of the value and that part hasn’t changed.

🔧 Code Example: Problematic useContext Usage
// context.js
export const AppContext = React.createContext();

export const AppProvider = ({ children }) => {
  const [count, setCount] = useState(0);
  const [theme, setTheme] = useState("light");

  return (
    <AppContext.Provider value={{ count, setCount, theme, setTheme }}>
      {children}
    </AppContext.Provider>
  );
};
// CounterComponent.jsx
const Counter = () => {
  const { count, setCount } = useContext(AppContext);
  console.log("Counter rendered");
  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
};

// ThemeComponent.jsx
const Theme = () => {
  const { theme, setTheme } = useContext(AppContext);
  console.log("Theme rendered");

  return (
    <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
      Theme: {theme}
    </button>
  );
};

❗ Problem:
Changing count will re-render ThemeComponent, even though it doesn’t use count.


That’s because useContext(AppContext) returns a new object every time any value changes.



✅ Solution 1: Split Contexts
Split your context into smaller, focused providers.
// CountContext.js
export const CountContext = React.createContext();
export const CountProvider = ({ children }) => {
  const [count, setCount] = useState(0);
  return (
    <CountContext.Provider value={{ count, setCount }}>
      {children}
    </CountContext.Provider>
  );
};

// ThemeContext.js
export const ThemeContext = React.createContext();
export const ThemeProvider = ({ children }) => {
  const [theme, setTheme] = useState("light");
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
};

Use them separately in components:
const Counter = () => {
  const { count, setCount } = useContext(CountContext);
  console.log("Counter rendered");
  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
};

const Theme = () => {
  const { theme, setTheme } = useContext(ThemeContext);
  console.log("Theme rendered");
  return <button onClick={() => setTheme("dark")}>Theme: {theme}</button>;
};


✅ Solution 2: Use useMemo in Context Provider
const value = useMemo(() => ({ count, setCount, theme, setTheme }), [count, theme]);

But this doesn’t fix the render problem — just stabilizes the reference.

✅ Solution 3: Use Selectors with Context (advanced)
With libraries like use-context-selector, you can avoid re-renders by selecting only part of the context. useSelector is used to access and subscribe to specific parts of the Redux store inside a React component. It allows components to re-render automatically when the selected state changes, helping avoid prop drilling and enabling efficient state management at a global level.
useSelector -  is a hook from React Redux that lets you read data from the Redux store inside a React component.
   useSelector automatically:
Subscribes to Redux store
Re-renders component when selected state changes
❗ Re-render happens when:
Selected value changes (by reference)
npm install use-context-select
import { createContext } from "use-context-selector";

const AppContext = createContext();
const Counter = () => {
  const count = useContextSelector(AppContext, ctx => ctx.count);
};

This way, components only re-render if their selected part changes.

🧠 Summary
                   Problem
            Solution
All consumers re-render on any change
Split contexts
Context value is an object → changes every render
Use useMemo
Need to optimize further
Use use-context-selector



When should you use React Context vs. Redux or other state management solutions for performance reasons ?
Answer -> 🧠 React Context vs Redux: Performance Considerations

⚛️ React Context
✅ Best when:
You need to share global but simple state, like:


Theme (light/dark)


Auth user info


Locale (language)


The state doesn't update frequently.


Your app is small to medium-sized.


⚠️ Performance concern:
Every component that consumes the context will re-render when the context value changes — even if the component doesn't use the updated part.


No built-in way to prevent unnecessary re-renders without extra memoization.


        🔧 Example issues:
              If you store a frequently-changing counter in Context:
<CounterContext.Provider value={{ count }}>

➡ Every component consuming count re-renders on every update, even if it doesn't care about count.

🧰 Redux (or Zustand, Jotai, Recoil, etc.)
✅ Best when:
You have a complex global state: many slices, interactions, async logic.


You need to track state changes, use dev tools, or time travel (Redux DevTools).


Selective updates: Components can subscribe to only the piece of state they care about (good performance).


You want centralized and predictable state flow.
⚡ Performance benefits:
Built-in mechanism for fine-grained updates


Selectors allow you to pick specific states, so fewer components re-render.


Middleware like redux-thunk or redux-saga helps handle async cleanly.



🆚 Summary Table
  Feature
React Context
Redux / Other Stores
Simplicity
✅ Very simple
❌ More setup required
Best for
Small apps / static data
Large apps / dynamic state
Selective re-renders
❌ All consumers re-render
✅ Fine-grained subscriptions
DevTools
❌ No built-in support
✅ Strong debugging tools
Async logic (API, etc.)
❌ Manual handling
✅ Built-in via middleware
Performance on large scale
❌ Gets worse with size
✅ Scales well


🟨 Real-world Recommendation
App Size
Recommendation
Small (1–2 pages)
                  React Context
Medium
                  Zustand or Redux Toolkit
Large (many pages/features)
                  Redux Toolkit + middleware                (like Thunk/Saga)


🧪 Bonus Tip
        If you still want to use Context but need performance, use:
  const CountContext = React.createContext();
  const CountProvider = ({ children }) => {
  const [count, setCount] = useState(0);
  const value = useMemo(() => ({ count, setCount }), [count]);
  return <CountContext.Provider value={value}>{children}</CountContext.Provider>;
};

And split context into multiple small providers (AuthContext, ThemeContext, etc.) instead of a "God Context."
How can you avoid unnecessary re-renders when using useEffect?


3. Rendering Optimization
How does React’s key prop help with performance in lists?
Ans - Keys give React a way to uniquely identify list items between renders, reducing unnecessary re-renders and preserving component state, which improves performance. Can give example of Virtual DOM tree creation in which the two same html element renders.
What are React.memo and PureComponent? How do they improve performance?


How do you handle expensive calculations in functional components efficiently?


When should you use lazy loading in a React application?


How does server-side rendering (SSR) improve performance in React?
SSR (Server-Side Rendering) is one of the core techniques in modern React (and other frontend frameworks) to improve performance, SEO, and user experience. Let’s break it down:1️⃣ What is SSR?
Normally, React apps use CSR (Client-Side Rendering):
Browser loads an empty index.html.


React JS bundle downloads, executes, and mounts components.


Until then, the user sees a blank page → bad for SEO & initial performance.


👉 SSR (Server-Side Rendering) fixes this by rendering the React components into HTML on the server before sending it to the browser.

2️⃣ How SSR Works (Step by Step)
Client Request → User requests a URL (/products).


Server Runs React Code → React is executed on the server.

 import { renderToString } from "react-dom/server";
import App from "./App";

const html = renderToString(<App />);
 This produces an HTML string.


Server Response → The server sends the HTML to the browser.

 <html>
  <body>
    <div id="root">
      <h1>Product List</h1>
      <ul><li>Product 1</li><li>Product 2</li></ul>
    </div>
    <script src="/bundle.js"></script>
  </body>
</html>
Hydration → Once the JS bundle loads, React takes over and hydrates the HTML (attaches event listeners, makes the page interactive).
Process -> Inside the SSR, when we request a page from server, it gives us the html to browser, then a process of hydration occurs in which react will attach the event listeners to the code provided by server.



3️⃣ Benefits of SSR
 ✅ Faster First Paint (users see content immediately).
 ✅ Better SEO (search engines can crawl fully rendered HTML).
 ✅ Better performance on slow devices/networks.

4️⃣ How SSR is Implemented in React
There are two ways:
               A. Custom SSR Setup
Use Express.js with react-dom/server.


Example:


// server.js
import express from "express";
import React from "react";
import { renderToString } from "react-dom/server";
import App from "./App";

const app = express();

app.get("*", (req, res) => {
  const html = renderToString(<App />);
  res.send(`
    <html>
      <head><title>SSR Example</title></head>
      <body>
        <div id="root">${html}</div>
        <script src="/bundle.js"></script>
      </body>
    </html>
  `);
});

app.listen(3000, () => console.log("SSR app running on http://localhost:3000"));

            👉 Here, server renders <App />, sends HTML, and client hydrates it.

B. Using Frameworks (Real-World Use)
Next.js → Built-in SSR support.


Remix → SSR-first framework.


Nuxt (Vue), SvelteKit → Same for other frameworks.


Example (Next.js):
export async function getServerSideProps() {
  const res = await fetch("https://dummyjson.com/products");
  const products = await res.json();
  return { props: { products } };
      }

export default function Products({ products }) {
  return (
    <ul>
      {products.map(p => <li key={p.id}>{p.title}</li>)}
    </ul>
  );
}

👉 Here, data fetching and rendering happen on the server.

5️⃣ SSR vs CSR vs SSG
Technique
Where Render Happens
Pros
Cons
CSR
Browser
Rich interactivity
Slow first paint, SEO issues
SSR
Server → Browser hydrates
SEO, faster load
Server load, slower TTFB
SSG (Static Site Generation)
Build-time
Fastest, CDN-ready
Not dynamic (needs revalidation)


             ✅ Summary
SSR = Render HTML on server, hydrate on client.


Implemented with react-dom/server (custom) or frameworks like Next.js.


Boosts SEO, improves first load, but adds server overhead.


4. Code-Splitting & Lazy Loading
What is code-splitting, and how does it improve React performance?
Ans -> 
🔹 What is Code-Splitting?
Code-splitting is a performance optimization technique where a React application’s JavaScript bundle is split into smaller chunks and loaded on demand, instead of loading the entire app at once.

🔹 Why is Code-Splitting needed?
Without code-splitting:
The browser downloads one large JS bundle


Initial load time increases


Slower performance, especially on low-end devices


With code-splitting:
Only required code is loaded initially


Remaining code is loaded when needed


Faster initial page load and better user experience



🔹 How does Code-Splitting improve performance?
   ✔️ Reduces initial bundle size
   ✔️ Faster Time to First Paint (TTFP)
   ✔️ Faster Time to Interactive (TTI)
   ✔️ Loads heavy components only when required
   ✔️ Improves perceived performance


How do you implement lazy loading in React using React.lazy and Suspense?
Ans -> 
import React, { Suspense, lazy } from "react";
const HeavyComponent = lazy(() => import("./HeavyComponent"));
function App() {
  return (
    <Suspense fallback={<div>Loading...</div>}>
      <HeavyComponent />
    </Suspense>
  );
}`

What are some strategies to optimize bundle size in React applications?
Ans -> 
Strategy


       Benefit
Code-Splitting (React.lazy(), Suspense, dynamic imports)


Loads only required components, reducing initial bundle size.
Tree Shaking


Eliminates unused code, keeping bundles lightweight.
Minimize Third-Party Libraries


Avoids bloated dependencies by using lighter alternatives.
Optimize Images & Lazy Load


Prevents loading unnecessary assets.
Enable Gzip/Brotli Compression


Reduces JS file sizes by ~70%.
Optimize Webpack Config (splitChunks, bundle analyzer)


Splits common libraries, analyzes bundle size.
Remove Unused CSS (PurgeCSS)


Keeps only necessary styles, reducing CSS file size.
Use Production Mode (NODE_ENV=production)


Removes dev-only React code, reducing bundle size.




How can you analyze and optimize Webpack bundle sizes in a React project?
Ans - npm install --save-dev webpack-bundle-analyzer
                     npm run build
Open a visual treemap in your browser.


Helps you find large modules, duplicate packages, unused libraries.


What tools can we use to measure performance bottlenecks in a React app?
Ans -> 
                 Tool
     Use Case
         Best For
React Profiler (DevTools)
Identifying slow components
Debugging unnecessary re-renders
Chrome Performance Tab
JavaScript execution time
Measuring layout shifts & reflows
Lighthouse
Page performance analysis
Improving load time, SEO, UX
WebPageTest
Network request analysis
Optimizing external resources
Bundlephobia
Checking npm package size
Reducing bloated dependencies
Webpack Bundle Analyzer
Visualizing JavaScript bundles
Removing unused code, tree shaking
Why Did You Render
Detecting unnecessary re-renders
Optimizing state & prop updates




5. React with Third-Party Libraries & Performance
How do third-party libraries impact React performance?
Ans -> 
Issue
Solution
Large Bundle Size
Use smaller alternatives, tree shaking, and code-splitting.
Unnecessary Re-renders
Use React.memo, useMemo, and useCallback.
Blocking UI (Heavy Computations)
Offload to Web Workers, debounce/throttle events.
Inefficient State Management
Use Reselect for Redux, prefer Context API for small apps.
Memory Leaks
Always clean up event listeners, WebSockets, and subscriptions.
Unused Dependencies
Run npx depcheck to remove unused packages

Web Workers - Web Workers are a browser feature that allows you to run JavaScript code in a separate background thread, without blocking the main UI thread.
JavaScript is single-threaded, meaning:
Long-running operations (e.g. data processing, image manipulation, complex loops) can freeze the UI.


Web Workers solve this by offloading heavy tasks to another thread.
22. How can you optimize performance when using a large number of third-party dependencies ?
Ans -> When using many third-party libraries in a React app, performance can degrade due to larger bundle sizes, unnecessary re-renders, memory leaks, and inefficient state updates.
Heavy Library
Lighter Alternative


moment.js (300 KB)
                    date-fns (50 KB)


lodash (70 KB)
lodash-es (tree-shakable)


react-select (25 KB)
headlessui (3 KB)


axios (5 KB)
fetch API (built-in)


What are some common performance pitfalls when integrating React with large data sets (e.g., infinite scrolling, virtual lists)?
Ans ->  ⚠️ Performance Pitfalls with Large Data Sets in React
Rendering Too Many DOM Nodes
 ➤ Use virtualization (react-window, react-virtualized).


Lack of Memoization
 ➤ Use React.memo, useMemo, useCallback.


Unstable or Duplicate Keys in Lists
 ➤ Use unique, stable keys (avoid using index as key).


Heavy Computation in Render
 ➤ Move logic out of render, use useMemo or web workers.


Unthrottled Scroll/Event Handlers
 ➤ Throttle or debounce scroll and resize events.


Loading Too Much Data at Once
 ➤ Implement pagination or infinite scroll.


Using Global State for Large Lists
 ➤ Keep large state local or use granular state libraries (e.g., Zustand).


Inefficient Filtering/Search on Large Lists
 ➤ Use useMemo, debounce inputs, or perform filtering asynchronously.


No Lazy Loading / Code Splitting
 ➤ Use React.lazy, Suspense, and dynamic imports.


Multiple State Updates Without Batching
 ➤ Batch updates where possible to avoid extra re-renders.



How can you optimize a React app when dealing with frequent API calls?
Ans -> ⚡ Optimizing React Apps with Frequent API Calls
Debouncing / Throttling


Delay API calls until user stops typing (debounce)


Limit calls over time (throttle)


✅ Use lodash.debounce, lodash.throttle, or custom hooks
IT IS USED IN GOOGLE DOCS - WHEN USER STOPS TYPING IT SAVES IT AUTOMATICALLY


Prevent Unnecessary Re-renders


React.memo() to memoize components


useCallback() to memoize functions


useMemo() to cache expensive computations


Cache API Results


Store fetched data in state, context, or custom hooks


🛠 Use tools like:


React Query


SWR


Apollo Client


Abort Previous Requests


Use AbortController to cancel ongoing requests on input change or unmount


Server-side Pagination & Filtering


Fetch only the data needed (paged, filtered, sorted) from the server


Batch API Calls


Combine multiple calls into one using Promise.all or batch endpoints


Lazy Load Components & Data


Use React.lazy, Suspense, or dynamic imports to load components only when needed


How does React handle event delegation, and how can it improve performance?
Ans -> 🚀 Performance Benefits
Fewer Event Listeners


Only one listener per event type → reduces memory usage.


Efficient Memory Usage


Avoids the overhead of attaching/detaching listeners for each component.


Faster Mounting & Unmounting


No need to manage multiple event bindings manually.


Simplified Cleanup


React handles cleanup automatically during unmounting or re-renders.


Consistent Cross-browser Behavior


Synthetic events normalize differences in native events across browsers.
6. Server-Side & Client-Side Optimization
How does Next.js improve performance compared to a standard React app?
Ans -> Next.js improves performance compared to a standard React app through several built-in optimizations:
Server-Side Rendering (SSR):


Pre-renders pages on the server to speed up initial load times and improve SEO.


Static Site Generation (SSG):


Generates static HTML at build time for faster delivery of content, ideal for pages that don’t change often.


Incremental Static Regeneration (ISR):


Updates static content on-demand in the background, combining the benefits of static and dynamic rendering.


Automatic Code Splitting:


Breaks your code into smaller chunks, loading only what’s necessary for each page, which reduces the overall bundle size.


Optimized Image Handling:


The built-in next/image component optimizes images by lazy-loading and resizing them, enhancing performance.


Built-in Caching & Prefetching:


Automatically prefetches linked pages in the background and implements caching strategies to reduce load times.


Enhanced Data Fetching:


Uses methods like getStaticProps and getServerSideProps to fetch data more efficiently, ensuring only necessary data is loaded.


What are the benefits of preloading and prefetching assets in React?
Ans -> 🔹 Preloading & Prefetching Improve:
Performance


Loads critical or likely-to-be-used assets earlier.


Reduces delays in rendering or interaction.


Page Transition Speed


Prefetched components/routes load instantly on navigation.


Improves perceived performance.


User Experience (UX)


Faster load times and smoother navigation.


Makes the app feel more responsive.


Network Efficiency


Uses browser idle time to fetch assets.


Prevents blocking of essential rendering.


Reduced Latency


Assets are ready before the user explicitly needs them.


How can you optimize images and assets in a React application?
   	Ans -> 🖼️ Image Optimization
Use Modern Formats


Prefer formats like WebP, AVIF over JPEG/PNG for better compression and quality.


Lazy Loading


Load images only when they enter the viewport.


Use native loading="lazy" or libraries like react-lazyload or react-intersection-observer.


Responsive Images


Use srcSet and sizes attributes to serve images based on screen size and resolution.


Image Compression


Compress images using tools like TinyPNG, ImageOptim, or webpack plugins before bundling.


Use CDN


Serve static assets from a CDN to reduce load time and latency.


How does service worker caching improve React app performance?
Ans -> ⚡ Service Worker Caching Benefits in React
🔁 Faster load times – Loads assets from cache instead of network


🌐 Offline support – App works even without internet


📉 Reduced network usage – Minimizes repeated API/asset requests


🔄 Background updates – Fetches and caches new data silently


✅ Better UX – More reliable and smooth experience



What are some strategies for improving Time to Interactive (TTI) in a React app?
Ans -> ⚡ Strategies to Improve TTI in React
🧱 Code Splitting


Load only necessary code per route using React.lazy() or dynamic imports.


⏳ Lazy Loading


Delay loading of images, components, and non-critical resources.


🚀 Use React.memo & useCallback


Prevent un-necessary re-renders to keep interactions snappy.


🔧 Minimize JavaScript Bundles


Remove unused code with tree shaking and reduce third-party dependencies.


📦 Use a CDN for Static Assets


Serve JS/CSS/images from a CDN to reduce load time.


🛑 Defer Non-Critical Scripts


Use async or defer attributes for third-party scripts (e.g., analytics).


📉 Optimize API Calls


Debounce frequent calls and cache responses when possible.


🖼️ Optimize Images


Use compressed and responsive image formats like WebP or AVIF.


📄 Preload Key Resources


Use <link rel="preload"> for fonts and important scripts.


🧠 Reduce Main Thread Blocking


Avoid heavy computations on the main thread; offload to Web Workers if needed.
🔁 Debouncing vs Throttling
Feature
Debouncing
Throttling
📌 Definition
Delays execution until a specified time has passed since the last call
Ensures a function is executed once every specified interval
⏳ Use case
Run after the user stops typing, scrolling, etc.
Run at regular intervals during a continuous event
🧠 Behavior
Only the final event is triggered
Triggers function at regular intervals
🧪 Example Scenario
Search input box (wait until user stops typing)
Logging mouse position while moving
🔄 Execution style
Delays and resets timer on each call
Ignores calls during cooldown window
✅ When it runs
Only once after the burst of events ends
Multiple times, but never more than once per delay


 REACT LIFECYCLE METHODS
⚛️ Lifecycle Equivalents in Functional Components
React Hooks provide the same capabilities:
Class Lifecycle
Functional Hook Equivalent
componentDidMount
useEffect(() => { ... }, [])
componentDidUpdate
useEffect(() => { ... }, [deps])
componentWillUnmount
useEffect(() => { return () => {...} }, [])
shouldComponentUpdate
React.memo() for components, useMemo() for value



Q- How does my browser read the JSX ??
Ans -> WITH HELP OF BABEL
Step 1 -> JSX is compiled (usually by Babel) into regular React.createElement calls.
Step 2 -> React.createElement creates a Virtual DOM node (a plain JavaScript object):

USE LAYOUT AND USEEFFECT
🧠 Basic Definitions

Flow of how react update the UI
Render Phase (Calculate JSX)
Commit Phase (Update Dom)
Browser Paints (Update UI)
🔵 useEffect
Runs after the browser paints the UI.
 It is asynchronous in behavior and is non-blocking.
useEffect(() => {
  // Side effects here
}, []);


🟠 useLayoutEffect
Runs synchronously after DOM mutations but before the browser paints.
 It blocks painting until it finishes, like componentDidMount but earlier.
useLayoutEffect(() => {
  // DOM reads/writes here
}, []);


🆚 Key Differences
         Feature
   useEffect
   useLayoutEffect
Timing
After paint
Before paint
Blocking rendering
❌ No
✅ Yes (blocks paint)
Usage
API calls, subscriptions
Measure DOM, fix layout
Performance
More performant (async)
Can cause jank if overused
UI visible before run
✅ Yes
❌ No, runs before it's visible


🔎 Visual Example
useEffect(() => {
  console.log("useEffect");
});

useLayoutEffect(() => {
  console.log("useLayoutEffect");
});

Console output order:
useLayoutEffect
useEffect


💡 When to Use Each
           Use Case
    Hook to Use
Fetch data from API
useEffect
Set up subscriptions
useEffect
Update state after render
useEffect
Measure DOM size/position
useLayoutEffect
Perform animations right after DOM
useLayoutEffect
Prevent layout flickering
useLayoutEffect


⚠️ Important Note
Prefer useEffect unless you have a specific need to block the paint and access layout info.
 useLayoutEffect can harm performance if misused.

✅ Summary
   useEffect
  useLayoutEffect
Non-blocking, async
Blocking, sync
Runs after painting
Runs before painting
Good for side effects
Good for DOM measurements/fixes



 Q3: How do you add a custom button using @apply?
Answer:
 In your index.css:
.btn {
  @apply px-4 py-2 rounded bg-blue-500 text-white hover:bg-blue-600;
}

You can now use <button class="btn">Click</button> in your HTML/JSX.

🔸 Q5: How can you add a custom color or font in Tailwind?
Answer:
 Edit tailwind.config.js:
theme: {
  extend: {
    colors: {
      brand: '#1e40af',
    },
    fontFamily: {
      sans: ['Inter', 'sans-serif'],
    },
  },
},
Then use bg-brand or font-sans in your components.
 Q8: How do you handle dark mode in Tailwind?
Answer:
 Enable in config:
darkMode: 'class', // or 'media'
Then use:
<div class="bg-white dark:bg-gray-900 text-black dark:text-white">
You can toggle the dark class on <html> or <body> using JavaScript or theme settings.

 Q9: What are plugins in Tailwind? Have you used any?
Answer:
 Tailwind plugins are used to extend functionality. Examples:
npm install @tailwindcss/forms @tailwindcss/typography

plugins: [
  require('@tailwindcss/forms'),
  require('@tailwindcss/typography'),
]

They add utility classes for form controls and rich content styling (e.g., prose classes).


WORKING OF USE-CALLBACK

✅ Purpose of useCallback in React:
useCallback is a React Hook that returns a memoized version of a callback function, which only changes if one of its dependencies has changed.

💡 Problem It Solves
Without useCallback, every time a component re-renders, all functions defined inside it are re-created — even if their logic or dependencies haven’t changed.
This causes:
Unnecessary re-renders of child components (especially when passing callbacks as props).


Performance degradation in large applications.



✅ useCallback — Short & Clear Summary
useCallback memoizes the function reference, not the function logic.


Without useCallback, a new function object is created on every render.


With useCallback, React reuses the same function reference until dependencies change.



🧠 Why it improves performance (despite using memory)
Memory is cheap, but re-renders are expensive.


useCallback trades a tiny amount of memory to:


Prevent unnecessary child re-renders


Avoid re-running effects


Reduce reconciliation work


👉 It does not make the function faster.
 👉 It prevents unnecessary renders.

🚀 Where useCallback actually helps
With React.memo


Prevents child components from re-rendering due to changing function references.


In dependency arrays


Stabilizes dependencies for useEffect / useMemo.

❌ When NOT to use it
Internal functions not passed as props


Small components with no memoized children


Blind usage everywhere



🏆 Perfect Interview Answer
useCallback memoizes the function reference so React can reuse it across renders. Although it uses memory, that cost is negligible compared to avoiding unnecessary re-renders. It improves performance mainly when passing callbacks to memoized components or using them in dependency arrays.”

🔑 One-Line Rule
useCallback doesn’t optimize execution — it optimizes re-rendering.

✅ Syntax
const memoizedCallback = useCallback(() => {
  // function logic
}, [dependencies]);

📌 Example Without useCallback
import React, { useState } from "react";

function Child({ onClick }) {
  console.log("Child Rendered");
  return <button onClick={onClick}>Click Me</button>;
}

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    console.log("Clicked");
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <Child onClick={handleClick} />
    </div>
  );
}

❌ Problem:
Every time you click "Increment", Parent re-renders, which recreates the handleClick function, causing the Child component to re-render too — even though it doesn’t need to.

✅ Fixed with useCallback
import React, { useState, useCallback } from "react";
const Child = React.memo(({ onClick }) => {
  console.log("Child Rendered");
  return <button onClick={onClick}>Click Me</button>;
});

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <Child onClick={handleClick} />
    </div>
  );
}

✅ Result:
Now, when you click "Increment", Child won't re-render because handleClick reference stays the same.

⚠️ Disadvantages / When not to use useCallback
Memory overhead:


It stores memoized functions in memory. Overusing useCallback can increase memory usage.


Unnecessary complexity:


If you're not passing the function to children or not optimizing performance, using it adds unnecessary code.


False optimization:


If the function is cheap to recreate and not used as a prop, memoization gives no benefit and might slightly hurt performance.



🧠 When To Use useCallback
Use useCallback only when:
You're passing the function as a prop to a memoized child (e.g., using React.memo()).


The function is expensive to recreate.


You want to prevent unnecessary effects/triggers caused by function identity change.



✅ Summary
       Aspect
                       Description
What it is
React Hook to memoize functions
Fixes
Prevents unnecessary re-renders caused by new function references
Use with
React.memo, useEffect, performance optimization
Avoid when
Not passing function as a prop or the function is trivial



WORKING OF USE-MEMO
✅ Purpose of useMemo in React
useMemo is a React Hook that memoizes the result of an expensive computation — it only recalculates the value when one of its dependencies changes.

💡 Problem It Solves
In React, during each re-render:
All functions and values inside the component are re-evaluated.
If you have a computationally expensive calculation, it will be recalculated on every render — even if its input hasn’t changed.


This causes:
Performance issues.


Unnecessary calculations.



✅ Syntax
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);


📌 Example Without useMemo
import React, { useState } from "react";

function expensiveCalculation(num) {
  console.log("Calculating… >>", num);
}

function App() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  const result = expensiveCalculation(count); // recalculates every render

  return (
    <div>
      <h1>Expensive Result: {result}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
    </div>
  );
}

❌ Problem:
Even if you just type in the input box (which has nothing to do with count), the expensiveCalculation() still runs, causing lag.

✅ Fixed with useMemo
import React, { useState, useMemo } from "react";

function expensiveCalculation(num) {
  console.log("Calculating… >>", num);
}

function App() {
  const [count, setCount] = useState(0);
  const [input, setInput] = useState("");

  const result = useMemo(() => expensiveCalculation(count), [count]);

  return (
    <div>
      <h1>Expensive Result: {result}</h1>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <input value={input} onChange={(e) => setInput(e.target.value)} />
    </div>
  );
}

✅ Result:
Now, the expensive function only runs when count changes — not when typing in the input box.

⚠️ Disadvantages / When not to use useMemo
Memory Overhead:


useMemo stores the previous return value and dependencies — adds memory pressure if overused.


Added Complexity:


Makes your code harder to read if used unnecessarily.


Negligible Performance Benefit:


If the computation is cheap or rerenders are infrequent, memoization adds more overhead than it saves.


Stale Values:


Can cause bugs if the dependency array is incomplete or inaccurate.



🧠 When To Use useMemo
Use it when:
You have a heavy calculation that shouldn't run on every render.


You are rendering lists or filtered data that doesn’t change often.


You want to optimize re-renders for derived data.



✅ Summary
     Aspect
           Description
What it is
React Hook to memoize computed values
Fixes
Prevents re-execution of heavy calculations on every render
Use with
Expensive functions, derived state, filtered lists
Avoid when
Calculation is fast or dependencies change frequently


FORWARD REF
forwardRef is a React utility that lets you pass a ref from a parent component to a child component, especially when the child is a functional component.
By default, refs don’t get passed through functional components — forwardRef allows that.
Example: Focus Input from Parent
const MyInput = forwardRef((props, ref) => {
  return <input ref={ref} {...props} />;
});

function Parent() {
  const inputRef = useRef();

  const handleClick = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <MyInput ref={inputRef} />
      <button onClick={handleClick}>Focus Input</button>
    </>
  );
}


❌ When You Don’t Need It
If you’re not exposing the DOM or a component's internal method to the parent.


If ref is used only internally within a component.


If you’re using state lifting or controlled components for interactivity.



⚠️ Things to Note
forwardRef makes your component less “pure” — it's exposing implementation details (like refs) to the parent.


Combine it carefully with useImperativeHandle if you want to expose custom instance methods instead of just a DOM ref.



  			REDUX-EXAMPLE

Link -> https://blog.logrocket.com/understanding-redux-tutorial-examples/


WORKING MODEL OF REDUX
Redux Toolkit is a third-party library that simplifies using Redux for state management in React applications.
Here's how it works:
When a user interacts with the UI (e.g., clicks a button), we dispatch an action using dispatch(). This action is an object with a type and optionally a payload.


The store receives the action and forwards it to the relevant reducer.


The reducer is a pure function that takes the current state and the action, and returns the new state.


The store updates with the new state and automatically re-renders any React components that are subscribed using useSelector.
Redux Toolkit makes this flow easier by using createSlice (to create reducers and actions together), and configureStore (to set up the store with middleware and dev tools by default).

Que-> Can we have the same name for a dispatcher method ?
Ans -> So, in a React application, if we have two store, which is known as CounterStore and CardStore, and we have App.jsx component inside that we are using the Counter, we are having the useSelector hook, it is used to get the current value of that particular state that we are trying to access, and we also have the useDispatch method. As soon as we call the Dispatch method on click of any button, then in that case, the imported method from their respective slice will run. We cannot have imports of similar names. Hence we can use the two stores in a single component.
🔐 Top Frontend Security Questions (with Answers)

1. What is XSS (Cross-Site Scripting)? How do you prevent it?
Answer:
 XSS happens when attackers inject malicious JavaScript into your page (usually through user input).
Prevention:
Escape/ sanitize user input


Use frameworks that auto-escape HTML (React, Angular)


Avoid dangerouslySetInnerHTML


Use Content Security Policy (CSP)


Validate inputs on backend



2. What is CSRF? How do you prevent it?
Answer:
 Cross-Site Request Forgery = attacker forces a logged-in user to perform actions (like money transfer).
Prevention:
CSRF tokens


SameSite cookies


Double-submit cookies


Use POST + custom headers


Validate origin and referer headers



3. What is CORS? Why is it used?
CORS = Cross Origin Resource Sharing.
 It controls which domains can call your API.
Used to prevent unauthorized cross-domain requests.
Key things:
browser enforces CORS, not server


preflight (OPTIONS) request happens for non-simple requests


solved by setting appropriate headers on server

4. What is Clickjacking? How to prevent it?
Attacker loads your site inside an invisible iframe and tricks the user to click.
Prevention:
X-Frame-Options: DENY / SAMEORIGIN


Content-Security-Policy: frame-ancestors 'none'



5. How do you safely render HTML in React/Vue?
Never directly insert untrusted HTML.
React:
dangerouslySetInnerHTML → only for sanitized HTML


Sanitization libraries like DOMPurify



6. Why should you avoid storing JWT tokens in localStorage?
Because JS-accessible storage is vulnerable to XSS.
Better alternatives:
HttpOnly Cookie


Secure Cookie


SameSite cookie

7. How to protect a Single Page Application (SPA) from URL tampering?
Since frontend can be modified:
Always validate permissions on backend


Role-based access must be enforced server-side


Never trust frontend checks like “isAdmin” flag



8. What is the difference between Authentication and Authorization?
 Authentication: Who are you?
 Authorization: What are you allowed to do?
Example:
  Login = authentication
  Access admin panel = authorization

9. What is Content Security Policy (CSP)?
Browser feature that blocks harmful scripts.
Example header:
Content-Security-Policy: default-src 'self'; script-src 'self';

Helps prevent:
XSS


unwanted scripts


inline JS



10. What is the security risk of using eval()?
eval() runs string as JavaScript code → huge XSS vector.
Avoid the front end completely.

11. How do you secure API calls from the front end?
Use HTTPS


Avoid exposing secrets in frontend


Use tokens with short expiry


Validate tokens on backend


Rate limiting



12. Can frontend code ever be fully secured?
No — frontend code can be inspected, modified, and reversed.
Therefore:
DO NOT put secrets (API keys)


DO NOT trust client-side validation


Always re-validate on backend



13. How do you detect malicious file uploads (images, PDFs)?
On frontend:
Restrict type (accept="image/*")


Restrict size


But security must be done on the backend.

14. What is HTTPS? Why is it important?
Encrypts request + response.
Prevents:
MITM attacks


Sniffing


Tampering



15. Why should API keys never be in frontend code?
Frontend is public → API key will be leaked.
 Solution:
Use env variables on backend


Proxy API requests via backend
16. React Internal Security Measures
React Internal Reconciliation Algorithm
Explanation with Example (from the video) - 
Mastering React Reconciliation - Advanced React course, Episode 6

Imagine you have a form where an input field conditionally renders based on a checkbox state. If the checkbox is checked (state = true), you render a business tax ID input; if unchecked (state = false), you render a personal tax ID input. Intuitively, you might expect that when toggling between these inputs, the typed text in one input would disappear when switching to the other, since they are different components.
However, React behaves differently: it preserves the typed text even after toggling. Why?
This happens because React’s reconciliation algorithm compares the Virtual DOM trees before and after the state update. When React compares these two input components:
The reference to the element changes (because a new element is created on each render),
But the component “type” remains the same (both are the same Input component),
React treats them as the same component instance and only updates the props (like placeholder or id), preserving the internal state such as the text typed inside. This leads to the unexpected behavior where the input text is preserved instead of being cleared.

Few Stuff to remember -> 
{
      item ? <input placeholder='Handle True Value'/> :  <input placeholder='Handle False Value'/>
    }

-> In this case my value remains intact because react creates a virtual DOM. Once we have typed something into the input box and then it checks via the shallow comparison, Behind the scenes shallow comparison does It just checks the attributes if the type of that component is same it just update the attribute and doesn't do anything with the value. We can fix it two ways.

Either by this:-
{
      item ? <input placeholder='Handle True Value'/> :  null
}

{
      !item ? <input placeholder='Handle False Value'/> :  null
}

Or by using the keys in it.

Reasoning -> Once we start using Keys, what react does it. The shallow comparison begins it just checks for the key And it finds that the keys are different then it totally re-mount the another componentLeading to the value disappear. 
How React Reconciliation Works (Key Points)
Virtual DOM Objects: React represents UI elements as objects with a type (string for DOM elements or function for components) and props.
Tree Comparison: On state updates, React creates a new Virtual DOM tree and compares it to the previous tree, node by node, position by position.
Shallow Comparison: If the object references are the same, React skips re-rendering that subtree.
Type Comparison: If the type changes between old and new objects, React unmounts the old component and mounts the new one, destroying internal state.
Same Type Update: If type is the same, React re-renders the component, updating props but preserving internal state.
Fixing the Input State Preservation Bug
Two common ways fix this:
Using Arrays with Null Placeholders:
Render your inputs as siblings in an array, swapping inputs by placing one as null and the other as a valid element in the array. React compares array positions and will unmount the input that changed from element-to-null and mount the other input, preserving the expected behavior.
Using Unique key Attributes:
Add a unique key prop to each input component that changes when the input conceptually changes (e.g., "business" vs "personal"). React uses keys to identify components uniquely in a list or array. When keys differ, React unmounts the previous component and mounts a new one, resetting state.
Why is key Important?
React uses key to identify components uniquely in a list or array.
Without keys, React compares components by their position in the array, which can cause unexpected state preservation or swapping.
With correct keys (e.g., unique IDs), React matches components correctly and preserves or resets state appropriately.
key does not prevent re-renders but helps React know which component corresponds to which item.


Interview-Ready Summary

React uses a process called reconciliation to efficiently update the UI by comparing a new Virtual DOM tree with the old one after state or prop changes. It decides whether to re-render, update, or remove components based on shallow comparisons and the component’s type. If the type stays the same, React updates the component’s props but preserves its internal state. If the type changes, React unmounts the old component and mounts a new one, resetting state.

A common pitfall occurs when conditionally rendering similar components without unique keys, resulting in unexpected state preservation (like input text staying when you expect it to clear). This happens because React thinks the component is the same due to the unchanged type.
To fix this, you should:
Use unique key props to help React differentiate components, or
Render conditional components in arrays with null placeholders so React can accurately mount/unmount components.
Understanding this concept allows you to write more predictable and performant React code, avoid subtle bugs, and optimize rendering behavior, which is crucial to mastering React’s internals and impressing interviewers.
JSON Example Illustrating React's Virtual DOM Objects and Reconciliation
Suppose you have a simple form component that conditionally renders an <Input> or a <Placeholder> component based on a boolean state (e.g., isBusiness).
When isBusiness is true:
json
{
  "type": "form",
  "props": {},
  "children": [
    {
      "type": "input",
      "props": {
        "id": "businessTaxId",
        "placeholder": "Enter Business Tax ID"
      },
      "children": []
    },
    {
      "type": "checkbox",
      "props": {
        "checked": true
      },
      "children": []
    }
  ]
}

When isBusiness is false:
{
  "type": "form",
  "props": {},
  "children": [
    {
      "type": "input",
      "props": {
        "id": "personalTaxId",
        "placeholder": "Enter Personal Tax ID"
      },
      "children": []
    },
    {
      "type": "checkbox",
      "props": {
        "checked": false
      },
      "children": []
    }
  ]
}
Key Points Illustrated by the JSON:
The Virtual DOM is a tree of objects representing React elements.
Each object has a "type" property, which is:
A string for DOM elements like "input", "form", "checkbox".
A function or reference for React components (not shown explicitly here but would be a function name).
"props" contains attributes like id, placeholder, or checked.
"children" is an array of child objects or empty if none.
How React Uses This JSON in Reconciliation:


Initial Render : React creates the above tree for isBusiness = true and mounts the input with business tax ID.
State Update (isBusiness toggled to false): React creates a new tree with the input having id: personalTaxId and compares it with the old tree.
Comparison Logic:
React compares nodes at the same position in the tree.
Since both are "input" types, React treats them as the same component and updates props (id, placeholder).
React does not unmount and remount the input component, so the internal state (like typed text) is preserved unexpectedly.
Fix Using key Attribute:
To force React to treat these inputs as different components and reset state, you add a key prop:
[
  {
    "type": "input",
    "key": "business",
    "props": {
      "id": "businessTaxId",
      "placeholder": "Enter Business Tax ID"
    },
    "children": []
  },
  {
    "type": "checkbox",
    "props": {
      "checked": true
    },
    "children": []
  }
]

vs.
json
[
  {
    "type": "input",
    "key": "personal",
    "props": {
      "id": "personalTaxId",
      "placeholder": "Enter Personal Tax ID"
    },
    "children": []
  },
  {
    "type": "checkbox",
    "props": {
      "checked": false
    },
    "children": []
  }
]

React now compares keys instead of just positions.
Different keys mean React unmounts the old input and mounts a new one.
The internal state resets, as expected.
Summary for Revision
React’s Virtual DOM represents UI as nested objects with type, props, and children.
During updates, React creates a new tree and compares it to the old tree positionally.
If types are the same and keys are missing or unchanged, React reuses the component instance, preserving internal state.
Adding unique key props helps React distinguish between components that appear similar, forcing unmount and remount to reset state.
This mechanism is crucial to understand bugs where input fields unexpectedly preserve or lose input on conditional rendering.
This JSON example encapsulates the core of React’s reconciliation and will help you visualize how React internally handles component updates, making it easier to explain and remember during interviews.


IMPORTANT  - IF REACT HAS GOT THE SAME REFERENCE, THEN IT WILL NOT RE-RENDER THE COMPONENT AT ALL.

Example - 
// ❌ Mutating state directly — React doesn't detect this
const [user, setUser] = useState({ name: "Alice", age: 25 });

user.name = "Bob"; // same reference → React sees no change → no re-render

// ✅ New reference — React detects the change
setUser({ ...user, name: "Bob" }); // new object → re-render ✅

// Same with arrays
const [items, setItems] = useState([1, 2, 3]);
items.push(4);               // ❌ mutates — no re-render
setItems([...items, 4]);     // ✅ new array — re-render


  REACT ARCHITECTURE PATTERNS
React architecture is about how components, state, data flow, and code patterns are structured so that apps remain scalable, maintainable, and performant, using patterns like component-based design, hooks, HOCs, Context API, code splitting, and testing.
🧩 Slide 1: What is React Architecture?
React Architecture defines:
How components are structured


How data flows


How state is managed


How scalability & performance are ensured


🎯 Goal: Maintainable, scalable, performant frontend

🧱 Slide 2: Component-Based Architecture
UI is broken into small reusable components


Each component:


Has a single responsibility


Can be tested independently


Encourages separation of concerns


📌 Example:
Page
 ├── Header
 ├── Sidebar
 └── Content
     ├── Card
     └── Button


🔁 Slide 3: Unidirectional Data Flow
Data flows top → down


Parent → Child via props


Child → Parent via callbacks


✅ Benefits:
Predictable state


Easier debugging


Fewer side effects



📦 Slide 4: State Management Layers
1️⃣ Local State
useState, useReducer


UI-specific state


2️⃣ Shared / Global State
Context API


Redux / Zustand / Recoil


🎯 Rule of Thumb:
Keep state as close as possible to where it’s used

🎨 Slide 5: Container vs Presentational Pattern
Presentational Components
UI only


No business logic


Reusable & dumb


Container Components
Data fetching


State management


Business logic


📌 Improves:
Testability


Readability


Maintainability



🔄 Slide 6: Reusability Patterns
🔹 Higher Order Components (HOC)
withAuth(Component)

Adds extra behavior


🔹 Render Props
<DataProvider render={(data) => <UI data={data} />} />

🔹 Custom Hooks (Preferred)
useFetch()
useAuth()
⭐ Modern React prefers Custom Hooks

🧠 Slide 7: Hooks-Driven Architecture
Hooks replace class lifecycle patterns:
useState → state


useEffect → side effects


useContext → global data


useReducer → complex logic


📌 Custom Hooks:
Extract reusable logic


Improve readability


Reduce duplication



🌍 Slide 8: Context API Usage
Used for:
Theme


Authentication


Language


Feature flags


⚠ Avoid:
Large frequently changing data


Performance-critical updates


👉 Otherwise use Redux/Zustand

⚡ Slide 9: Performance Optimization Patterns
React.memo


useMemo


useCallback


Virtualized lists


Debouncing / Throttling


🎯 Prevent:
Unnecessary re-renders


Heavy computations on every render



✂ Slide 10: Code Splitting & Lazy Loading
const Dashboard = React.lazy(() => import('./Dashboard'))

Load components on demand


Reduce initial bundle size


Faster first paint


Used heavily in:
Routes


Large components


Micro-frontends



🧪 Slide 11: Testing Strategy
Levels of Testing:
Unit Tests → Components & hooks


Integration Tests → Component interactions


E2E Tests → User flows


🛠 Tools:
Jest


React Testing Library


Cypress / Playwright



🏗 Slide 12: Folder Structure (Recommended)
src/
 ├── components/
 ├── pages/
 ├── hooks/
 ├── services/
 ├── store/
 ├── utils/
 ├── styles/

📌 Feature-based structure scales best for large apps

🚀 Slide 13: Scalable Architecture Principles
Keep components small


Avoid prop drilling


Prefer composition over inheritance


Separate business logic from UI


Optimize before premature optimization



🧠 Slide 14: Interview Power Answer
If interviewer asks:
“How do you architect a React application?”
Say this 👇:
“I follow a component-based architecture with unidirectional data flow, use local state wherever possible, Context or Redux for shared state, custom hooks for reusable logic, code splitting for performance, and memoization to prevent unnecessary renders. I structure the app feature-wise and ensure scalability with proper testing and optimization.”
🔥 That’s a senior-level answer

		MICRO-FRONTEND INTERVIEW QUESTIONS

Explain the architecture of micro-frontends.
Micro-frontend architecture = Shell + Independent MFEs + Integration Layer. You can implement via client-side, server-side, build-time, or hybrid approaches. The key is balancing independent deployments with consistent user experience.
How do you handle shared dependencies across MFEs?


What problems can occur if you load multiple versions of React? How do you solve it?


How do you ensure UX consistency across MFEs built by different teams?


Explain how Webpack Module Federation works.


How do MFEs communicate without tight coupling?


What are the trade-offs between SSR + Micro-frontends?


How would you migrate an existing monolith React app into MFEs?


How do you secure MFEs from version mismatches or broken deployments?


When not to use micro-frontends?




MACHINE CODING ROUND FRONTEND 

📌 Machine Coding Round – Frontend (3+ Yrs Experience)
🔹 1. UI Widgets / Components
These are the most common problems:
Autocomplete / Search Suggestions Component
 (e.g., type in a search box, show matching results with keyboard navigation & debounce)
-> Link - https://codesandbox.io/p/sandbox/auto-complete-qzqw9w


Accordion / Expandable Panel
 (click to expand/collapse, only one open at a time, handle nested accordions)


Tabs Component
 (switch between multiple tabs, preserve state in each tab)


Modal / Popup Component
 (with open/close functionality, click outside to close, escape key support)


Toast / Notification System
 (show success/error messages with auto-dismiss timers & stacked layout)


Star Rating Component
 (hover + select, half-stars, read-only mode)


Pagination Component
 (prev/next buttons, page numbers, dynamic page size, edge cases)



🔹 2. Stateful Components
Stopwatch / Timer App
 (start, pause, reset, lap times, countdown)


Todo App / Task Manager
 (CRUD operations, filtering [All/Completed/Pending], localStorage persistence)


Form Builder
 (dynamic form fields with validations and error handling)


Shopping Cart Component
 (add/remove items, update quantity, calculate total, discount logic)



🔹 3. Data Fetching + State Management
Search with Debouncing + API Integration
 (use setTimeout/clearTimeout or RxJS, show loading/error states)


Infinite Scroll / Lazy Loading
 (fetch next page of data as user scrolls near bottom)


Table with Sorting & Filtering
 (sortable columns, search filter, pagination, API-backed data)


Github Repo Search (or Movies List)
 (fetch from API, list results, paginate, add to favorites)



🔹 4. Complex UI Challenges
Multi-Select Dropdown with Search
 (select multiple options, remove selected items, keyboard support)


Drag and Drop List / Kanban Board
 (drag to reorder, move between lists, persistence)


Image Carousel / Slider
 (auto-play, manual navigation, infinite loop)


Nested Comments System (like Reddit/YouTube)
 (reply to comments, expand/collapse threads, recursion)



🔹 5. Design & Architecture Oriented
At 3+ years, interviewers expect clean code structure:
Implement custom hooks (React) for reusable logic
 (e.g., useFetch, useDebounce, useLocalStorage)


Manage state across components (Context API, Redux, Zustand, or custom solution)


Follow folder structure & modular code instead of one big file


Write testable code (bonus if you add Jest/Cypress tests)


Handle edge cases (empty states, error states, loading indicators)



🔹 6. Tricky Real-Life Problems
Typeahead Search (with caching + API cancelation)


Rate Limiter (don’t allow button click more than N times/sec)


File Upload Component (with drag & drop, preview, progress bar)


Dark Mode Toggle (with persistence in localStorage)


Editable Table / Inline Editing


Calendar / Date Picker




Web vitals - https://medium.com/@augustusphyras/web-performance-core-web-vitals-inp-1acfaba9700a



               	 REACT ASSESSIBILITY
1. Why Accessibility Matters (The "Why" Question)
Interviewers often open with "Why should we care about accessibility?" — answer with:
It enables people with visual, auditory, motor, or cognitive disabilities to use your app
It is legally mandated by ADA (Americans with Disabilities Act) and WCAG (Web Content Accessibility Guidelines)
It improves overall app quality for ALL users — keyboard users, slow-network users, elderly users
Accessibility is not an afterthought — it's an essential part of modern web development
2. Semantic HTML — Most Common Interview Question
"Why should you use semantic HTML?
// ❌ Bad — screen readers can't identify purpose
<div onClick={handleClick}>Click me</div>

// ✅ Good — browser + screen readers know it's interactive
<button onClick={handleClick}>Click me</button>

Use <header>, <main>, <nav>, <footer>, <section> — they are inherently recognized by screen readers without extra ARIA config.
Native HTML elements come with built-in keyboard support — a <button> responds to Enter and Space out of the box; a <div> does not

3. WAI-ARIA Attributes — Must Know
WAI-ARIA = Web Accessibility Initiative — Accessible Rich Internet Applications. It adds context to elements that semantic HTML alone can't describe.
Key ARIA attributes interviewers ask about:
Attribute
Purpose
Example
aria-label
Describes element when text isn't visible
Icon-only buttons like ✖ Close
aria-hidden
Hides decorative elements from screen readers
Icons, decorative images
aria-live
Announces dynamic content updates
Error messages, notifications
aria-expanded
Shows open/closed state
Dropdown, accordion
aria-modal
Marks a dialog as modal
Modal/Dialog components

// Icon-only button — screen reader would just say "button" without aria-label
<button aria-label="Close" onClick={handleClose}>✖</button>


4. Keyboard Navigation & Focus Management
This is a very common senior-level question — "How do you manage focus in a modal?"
const Modal = ({ isOpen, onClose }) => {
  const modalRef = useRef(null);

  useEffect(() => {
    if (isOpen) {
      modalRef.current.focus(); // trap focus inside modal when opened
    }
  }, [isOpen]);

  return isOpen ? (
    <div
      ref={modalRef}
      role="dialog"
      aria-modal="true"
      tabIndex="-1"   // makes non-interactive element focusable
    >
      <button onClick={onClose}>Close</button>
    </div>
  ) : null;
};

Key rules to remember:
All interactive elements must be reachable via Tab, Enter, Space, arrow keys
When a modal opens → focus must move into the modal
When a modal closes → focus must return to the trigger button
Use tabIndex="-1" to make a non-interactive element programmatically focusable (but not in tab order)

5. Accessible Forms
"How do you make forms accessible?" — answer covers.
// ✅ Always associate label with input using htmlFor
<label htmlFor="email">Email Address</label>
<input type="email" id="email" name="email" required />

// ✅ Announce form errors dynamically to screen readers
<div role="alert" aria-live="assertive">
  {formErrors.email && <span>{formErrors.email}</span>}
</div>

Use htmlFor (React's version of HTML for) to link label to input — without this, screen readers announce inputs with no context
Use role="alert" + aria-live="assertive" for real-time error announcements — critical for form validation UX

6. Focus Outlines — Never Remove Without Replacing
A mistake many developers make is removing focus outlines for aesthetic reasons.
css
/* ✅ Always keep or replace focus styles */
button:focus,
a:focus {
  outline: 2px solid #007bff;
  outline-offset: 2px;
}

/* ❌ Never just do this */
* { outline: none; }


7. Color Contrast — WCAG Numbers to Remember
Interviewers at product companies often ask about WCAG contrast ratios:
Normal text → minimum contrast ratio of 4.5:1
Large text (18px+ bold or 24px+) → minimum 3:1
Never use color alone to convey meaning (e.g., red = error) — always pair with an icon or text label

8. Testing Tools to Mention in Interviews
Always mention these when asked "How do you test accessibility?"
Lighthouse — built into Chrome DevTools, gives an accessibility score
Axe — browser extension for automated ARIA + semantic HTML violations
VoiceOver (Mac) / NVDA (Windows) — actual screen readers to manually test your app
Tab key test — the simplest test: navigate your entire app using only the keyboard

Dependency Graph - When webpack processes your app, it starts from an entry point and recursively maps every import/require to build a complete picture of what depends on what — that map is the dependency graph.
Extra Link - https://github.com/bafna-hitesh/Interview-preparation
