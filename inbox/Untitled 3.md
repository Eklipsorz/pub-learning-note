## 描述

> Unlike the stack, JavaScript stores objects (and functions) on the heap. The JavaScript engine doesn’t allocate a fixed amount of memory for these objects. Instead, it’ll allocate more space as needed.

> The following example defines the `name`, `age`, and `person` variables:


```javascript
let name = 'John';
let age = 25;

let person = {
  name: 'John',
  age: 25,
};
```

> Internally, the JavaScript engine allocates the memory as shown in the following picture:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-heap-memory.svg)


> In this picture, JavaScript allocates memory on the stack for the three variables `name`, `age`, and `person`.

> The JavaScript engine creates a new object on the heap memory. Also, it links the `person` variable on the stack memory to the object on the heap memory.

> Because of this, we say that the `person` variable is a reference that refers to an object.


### Dynamic properties

> A reference value allows you to add, change, or delete properties at any time. For example:
```javascript
let person = {
  name: 'John',
  age: 25,
};

// add the ssn property
person.ssn = '123-45-6789';

// change the name
person.name = 'John Doe';

// delete the age property
delete person.age;


console.log(person);
```

>Output:

`{ name: 'John Doe', ssn: '123-45-6789' }`

> Unlike a reference value, a primitive value cannot have properties. This means that you cannot add a property to a primitive value.

> JavaScript allows you to add a property to a primitive value. However, it won’t take any effect. For example:


```javascript
let name = 'John';
name.alias = 'Knight';

console.log(name.alias); // undefined
```

> Output:
`undefined`

> In this example, we add the `alias` property to the `name` primitive value. But when we access the `alias` property via the `name` primitive value, it returns `undefined`.


### Copying values

> When you assign a reference value from one variable to another, the JavaScript engine creates a reference so that both variables refer to the same object on the heap memory. This means that if you change one variable, it’ll affect the other.
> For example:

```javascript
let person = {
  name: 'John',
  age: 25,
};

let member = person;

member.age = 26;

console.log(person);
console.log(member);
```

> How it works.
>
> First, declare a `person` variable and initialize its value with an object with two properties `name` and `age`.
>
> Second, assign the `person` variable to the `member` variable. In the memory, both variables reference the same object, as shown in the following picture:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-copy-a-reference-value.svg)

> Third, change the `age` property of the object via the `member` variable:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-change-a-reference-value.svg)

> Since both `person` and `member` variables reference the same object, changing the object via the `member` variable is also reflected in the `person` variable.

## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 的 primitive data value 和 reference value 本身並不會有執行過程會變更大小的需求，所以會存放於stack記憶體區塊，並用變數名稱作為其區塊的識別名稱]]
References:
[[@javascripttutorialJavaScriptPrimitiveVs]]