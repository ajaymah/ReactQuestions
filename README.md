# ReactQuestions
### 1- How can decrese the bundle size in react app ### 

**Code Splitting (Lazy Loading)** - Load components only when needed instead of loading everything at once. 
```
import React, { Suspense, lazy } from "react";
const Dashboard = lazy(() => import("./Dashboard"));
```

