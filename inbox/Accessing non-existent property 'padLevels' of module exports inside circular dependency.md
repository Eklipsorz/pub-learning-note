
https://stackoverflow.com/questions/64713565/accessing-non-existent-property-padlevels-of-module-exports-inside-circular-de



> ## Solved Root Cause

> **exports inside circular dependency**

> 👆 This phrase gave hint to solve the same issue for me, it seems that newer NodeJS versions no longer allows circular dependencies.

> Eg - There are two files - FileA.js, FileB.js

> Where **FileA.js** has

```javascript
const FileB = require("FileB");
```

> and **FileB.js** has

```javascript
const FileA = require("FileA");
```

> After removing one of these circular dependencies by modifying either FileA.js or FileB.js, it was solved!