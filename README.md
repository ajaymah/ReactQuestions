# ReactQuestions
### 1- How can decrese the bundle size in react app ### 
  
- Code Splitting (React.lazy)  
- Dynamic Imports  
-Tree Shaking  
- Production Build  
- Remove unused dependencies  
- Bundle Analyzer  
- Lazy load routes  
- Optimize images & assets  

**Code Splitting (Lazy Loading)** - Load components only when needed instead of loading everything at once. 
```
import React, { Suspense, lazy } from "react";
const Dashboard = lazy(() => import("./Dashboard"));
```
**Dynamic Import** - Load modules dynamically.  
use - Useful for heavy libraries.  
```
import("./utils").then((module) => {
  module.myFunction();
});
```
**Tree Shaking**
```
import debounce from "lodash/debounce";
```  
**Remove Unused Libraries**  
Large libraries increase bundle size.

**Use Bundle Analyzer**  
A Bundle Analyzer helps you see which libraries are making your React bundle large. 
One common tool is webpack-bundle-analyzer.
```
npm install --save-dev webpack-bundle-analyzer
const { BundleAnalyzerPlugin } = require("webpack-bundle-analyzer");

module.exports = {
  plugins: [
    new BundleAnalyzerPlugin()
  ]
};
```

**Memoization**  
```
import React, { memo } from "react";

const MyComponent = memo(({ name }) => {
  return <div>{name}</div>;
});
```
**Use CDN for Large Libraries**  
**Optimize Images**  
**Use Lightweight Libraries**
| Heavy Library    | Lightweight Alternative |
| ---------------- | ----------------------- |
| moment.js        | dayjs                   |
| lodash           | lodash-es               |
| material-ui full | individual components   |

### 2- Error Boundary in React which case not working ###
**Error Boundary**  catches JavaScript errors in the component tree, but it does NOT work in some cases

**Error Boundary does NOT work in:**
-Event handlers  
-Async code (setTimeout, Promise)  
-Server-side rendering  
-Errors inside the error boundary itself  
-Errors outside the React component tree  
```
setTimeout(() => {
  throw new Error("Async Error");
}, 1000);
```

**Error Boundary only catches errors in:**  
- Rendering  
- Lifecycle methods  
- Constructors of child components
```
class ErrorBoundary extends React.Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h1>Something went wrong</h1>;
    }
    return this.props.children;
  }
}
```
> NOTE:
Error Boundaries can **catch errors from both class and functional components**, but the Error Boundary itself must be a class component.
>
```
function User() {
  throw new Error("User component crashed");
  return <h1>User</h1>;
}
///////////////
import React from "react";

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong</h2>;
    }

    return this.props.children;
  }
}
///////////////
<ErrorBoundary>
  <User />
</ErrorBoundary>
```
Error Boundaries require lifecycle methods like: componentDidCatch, getDerivedStateFromError  

### 3- What isSynthetic Event ###  
Synthetic Event is a cross-browser wrapper for the native DOM event provided by React.
```
function App() {

  const handleClick = (event) => {
    console.log(event);        // SyntheticEvent
    console.log(event.target); // clicked element
  };

  return <button onClick={handleClick}>Click Me</button>;
}
```
event is **not the native browser event**  
It is a **React SyntheticEvent**   

- **Why React Uses Synthetic Events**  
1️⃣ Cross-browser compatibility  
2️⃣ Same API for all browsers  
3️⃣ Better performance (event delegation)  
4️⃣ Easier event management  

**Example of Native Event vs Synthetic Event**  
**Native javaScript**  
```
document.getElementById("btn").addEventListener("click", function(e){
  console.log(e);
});
```
**React**  
```
<button onClick={(e) => console.log(e)}>
  Click
</button>
```
**e = SyntheticEvent**  
| React Event | Native Event |
| ----------- | ------------ |
| onClick     | click        |
| onChange    | change       |
| onSubmit    | submit       |
| onMouseOver | mouseover    |

**1- event.preventDefault()**
> Stops default browser behavior.  
```
function handleSubmit(e) {
  e.preventDefault();
}
```
**2- event.stopPropagation()**
> Stops event bubbling.
```
function handleClick(e){
  e.stopPropagation();
}
```

### 4- What is React and why is it efficient ###  
React is a JavaScript library used to build user interfaces. It is efficient because it uses a **Virtual DOM** and a reconciliation process to update only the changed parts of the UI, reducing direct DOM manipulations and improving performance. Its component-based architecture also promotes code reusability and maintainability.  

### 5- How does React work internally ###  
React converts JSX into JavaScript objects using React.createElement. These objects form the Virtual DOM. When state or props change, React creates a new Virtual DOM tree and compares it with the previous one using the reconciliation algorithm. React Fiber manages this process efficiently by prioritizing and scheduling updates. After identifying differences, React updates only the changed parts of the Real DOM during the commit phase, which makes React fast and efficient.

### 6- What is the most challenging task you handled in your project ###  
.....  

 

### 7- What is React Fiber   ###  
“React Fiber in React is the **internal reconciliation engine** that breaks rendering work into small units (fibers), allowing React to pause, resume,  
and prioritize updates.    
Before Fiber, React’s rendering process was synchronous:    
### 8- What is a “Fiber”? ###  
A Fiber is a **JavaScript object representing** a unit of work for a component.  

### 9 - How Fiber works ###
React fober - Rendering is split into two phases:  
 1 - **Render phase** (Reconciliation)  
 2 - **Commit phase**  

### 10 - What is code splitting ###  
**Code Splitting** is a performance optimization technique where a large JavaScript bundle is split into smaller chunks that are loaded on demand. In React, 
it can be implemented using **React.lazy()** and **Suspense**, while in Next.js it is commonly done using dynamic() imports. This reduces initial bundle size and improves page load performance.  
**Code Splitting** is a technique that breaks a large JavaScript **bundle** into smaller **chunks** that are loaded only when needed.   
**Example** without code splitting :  
```
import Home from './Home';  
import Dashboard from './Dashboard';  
import Admin from './Admin';  
```
**Example** With React.lazy()  
```
const Home = React.lazy(() => import('./pages/Home'));  
const About = React.lazy(() => import('./pages/About'));  
const Dashboard = React.lazy(() => import('./pages/Dashboard'));  
```

### 11- What is Lazy Loading? ###  
**Lazy Loading** is a performance optimization technique where resources (components, images, modules, etc.) are loaded only when they are needed, instead of loading everything    
 **Improve**  
 1-Initial page load time  
 2-Application performance  
 **Suspense** shows the fallback UI while loading.  
 **Benefits**  
✅ Faster initial page load  
✅ Reduced bundle size   
✅ Lower memory usage  
✅ Better Core Web Vitals  
✅ Improved user experience    

**Lazy Loading** is a technique where components, images, or modules are loaded only when they are required rather than during the initial page load. In React, it is commonly implemented using React.lazy() and Suspense. Lazy loading reduces the initial bundle size, improves page load performance, and enhances the user experience.

### 12- What is tree shaking ###  
**Tree Shaking** is a build optimization technique that removes unused code (dead code) from the final JavaScript bundle.  
Example-   
```
export const add = (a, b) => a + b;  
export const subtract = (a, b) => a - b;  
export const multiply = (a, b) => a * b;  

import { add } from './math';  
const math = require('./math');  
```
### 13- What is CORS? ###  
CORS (**Cross-Origin Resource Sharing**) is a browser security mechanism that controls whether one website can access resources from another website.
```
Access-Control-Allow-Origin: http://localhost:3000  
```
If the origin is allowed:    
✅ Response is accessible.   
If not:  
❌ Browser blocks access.   

CORS (Cross-Origin Resource Sharing) is a **browser security feature** that restricts web pages from making requests to a different origin unless the server explicitly allows it through CORS headers. It helps protect users from unauthorized cross-site requests while enabling controlled communication between different domains.  

### 14- What are stale closures in React ###
A **stale closure** happens when a function "remembers" an **old value of state or props** because it was created during an earlier render.  
A stale closure occurs when a function captures old state or props from a previous render and continues using those outdated values.   
This commonly happens in setInterval, setTimeout, event listeners, and effects with incorrect dependency arrays.  
It can be fixed by using the correct dependencies, functional state updates, or useRef to access the latest value.  

### 15- Explain optimistic UI updates ###  
Optimistic UI Updates are a technique where the UI is updated immediately before the server confirms the action  
Instead of waiting for an API response, the application assumes the request will succeed and updates the UI instantly. If the request later fails, the UI is rolled back 
```
const handleLike = async () => {  
  setLikes(prev => prev + 1);  

  try {  
    await api.likePost(postId);  
  } catch (error) {  
    setLikes(prev => prev - 1);  
  }  
};  
```
Optimistic UI updates are a technique where the UI is updated immediately before receiving server confirmation,  

### 16- what UI rendering methods, ###  
1- **CSR (Client-Side Rendering)**  
CSR renders the UI in the browser after JavaScript loads.   
**Use Cases:** Admin panels, Analytics dashboards   

2- **SSR (Server-Side Rendering)**  
 SSR renders HTML on the server for every request, improving SEO and initial load time.  
**Use Cases:** Blogs, News websites,E-commerce product, Better SEO, Good user experience  

3- **SSG** (Static Site Generation)  
SSG generates pages at build time and serves static HTML, making it very fast.
Pages are generated at build time.  
Extremely fast  
Excellent SEO  
**Use Cases:** Documentation sites, Marketing pages, Portfolio websites  

4- **ISR** (Incremental Static Regeneration)  
Static pages that can regenerate after deployment. 
ISR extends SSG by regenerating pages in the background at specified intervals 
Fresh data like SSR  
Use Cases: E-commerce catalogs, Product pages, Blogs with frequent updates  

### 17 -

