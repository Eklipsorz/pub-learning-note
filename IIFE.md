

## 描述
[[@mdnIIFEMDNWeb]] 所描述的IIFE
> An IIFE (Immediately Invoked Function Expression) is a JavaScript function that runs as soon as it is defined


```
// function IIFE
(function () {
  /* … */
})();
```


```
//  Anonymous function IIFE
(function () {
  /* … */
})();
```

```
//  Arrow function IIFE
(() => {
  /* … */
})();
```

```
//  Async IIFE
(async () => {
  /* … */
})();
```


> It is a design pattern which is also known as a Self-Executing Anonymous Function and contains two major parts:

> The first is the anonymous function with lexical scope enclosed within the Grouping Operator (). This prevents accessing variables within the IIFE idiom as well as polluting the global scope.

> The second part creates the immediately invoked function expression () through which the JavaScript engine will directly interpret the function.

重點


### function 是 expression ?


### Grouping operator


> [[@mdnGroupingOperatorJavaScript]]

> The grouping operator `( )` controls the precedence of evaluation in expressions.


> The grouping operator consists of a pair of parentheses around an expression or sub-expression to override the normal operator precedence so that operators with lower precedence can be evaluated before an operator with higher precedence. As it sounds, it groups what's inside of the parentheses. 



```
const a = 1;
const b = 2;
const c = 3;

// default precedence
a + b * c     // 7
// evaluated by default like this
a + (b * c)   // 7

// now overriding precedence
// addition before multiplication
(a + b) * c   // 9

// which is equivalent to
a * c + b * c // 9
```


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@mdnIIFEMDNWeb]]
[[@mdnGroupingOperatorJavaScript]]
