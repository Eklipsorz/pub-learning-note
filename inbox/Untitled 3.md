## 描述

[[@javascripttutorialJavaScriptPrimitiveVs]]
> When you declare variables, the JavaScript engine allocates the memory for them on two memory locations: stack and heap.

> Static data is the data whose size is fixed at compile time. Static data includes:
> - Primitive values (null, undefined, boolean, number, string, symbol, and BigInt)
> - Reference values that refer to objects.



> Because static data has a size that does not change, the JavaScript engine allocates a fixed amount of memory space to the static data and store it on the stack.



```javascript
let name = 'John';
let age = 25;
```
> Because `name` and `age` are primitive values, the JavaScript engine stores these variables on the stack as shown in the following picture:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-stack-memory.svg)

> Note that strings are objects in many programming languages, including Java and C#. However, strings are primitive values in JavaScript.



## Copying values
[[@javascripttutorialJavaScriptPrimitiveVs]]
> When you assign a primitive value from one variable to another, the JavaScript engine creates a copy of that value and assigns it to the variable. For example:

```javascript
let age = 25;
let newAge = age;
```

> Code language: JavaScript (javascript)

> In this example:

> -   First, declare a new variable `age` and initialize its value with `25`.
> -   Second, declare another variable `newAge` and assign the `age` to the `newAge` variable.

> Behind the scene, the JavaScript engine creates a copy of the primitive value `25` and assign it to the `newAge` variable.

> The following picture illustrates the stack memory after the assignment:


[![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-copy-a-primitive-value.svg)](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-copy-a-primitive-value.svg)

> On the stack memory, the `newAge` and `age` are separate variables. If you change the value of one variable, it won’t affect the other.

> For example:
```javascript
let age = 25;
let newAge = age;

newAge = newAge + 1;
console.log(age, newAge);
```


[![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-change-a-primitive-value.svg)](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-change-a-primitive-value.svg)





## 複習

---
Status: #🌱 
Tags:
Links:
References:
[[@javascripttutorialJavaScriptPrimitiveVs]]