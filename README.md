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



