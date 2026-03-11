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




