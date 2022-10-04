## 描述

### reference value & heap memory

> Unlike the stack, JavaScript stores objects (and functions) on the heap. The JavaScript engine doesn’t allocate a fixed amount of memory for these objects. Instead, it’ll allocate more space as needed.


重點：
- 由於物件本身會因為屬性會在執行期間進行任何變動，所以會將物件內容本身儲存在heap記憶體區塊，然後並於stack記憶體區塊儲存對應heap 記憶體位址




#### 案例

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


重點：
- name 和 age 本身是沒有執行時會變更記憶體區塊大小需求的primitive data value，所以會直接被存在stack記憶體區塊，他們記憶體區塊的名稱會分別為person、age。
```javascript
let name = 'John';
let age = 25;
```
- 在這裡由於是擁有執行時會變更記憶體區塊大小需求的物件，所以會於heap 記憶體區塊儲存以下內容，並於stack記憶體建立一個區塊來儲存該物件在heap的記憶體位址，stack記憶體區塊會被命名為person。
	- \{name: "John", age: 25\}
```javascript
let person = {
  name: 'John',
  age: 25,
};
```

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

重點：
- JS的物件本身定調為會在執行過程中變更其物件內容所佔取的記憶體區塊大小，所以可以在執行時增加、移除、修改屬性名和屬性值
- JS的primitive value本身定調為固定大小且不允許在執行過程變更其記憶體區塊，所以不能在執行時對記體體區塊做出新增、移除、修改屬性名和屬性值的動作，或者不能調整記憶體區塊的大小




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

重點：
- 多個儲存物件內容的記憶體區塊傳遞方式：由於識別字會是以stack記憶體區塊為主，所以會建立一個stack記憶體區塊來儲存另一個被複製過來的reference value，其值為對應heap記憶體位址。
- 當從另一個專門儲存object內容的變數A複製其值至另一個變數B時，JS引擎由於會以stack 記憶體區塊名稱來表示物件，語法會是：
	```
	variableA = variableB
	```
	- 以reference value大小來製作一個固定大小的新stack記憶體區塊
	- 接著把變數A的對應reference value複製至新stack記憶體區塊，並為記憶體區塊設定對應名稱為變數B
	- 在這裡變數A和變數B都會因為相同的reference value而指向相同的物件
		- 這使得可透過變數A和變數B來調整相同的heap 記憶體區塊


## 複習
#🧠 JS中，物件如何在記憶體儲存？請說明 ->->-> `由於物件本身會因為屬性會在執行期間進行任何變動，所以會將物件內容本身儲存在heap記憶體區塊，然後並於stack記憶體區塊儲存對應heap 記憶體位址`

#🧠 let person = \{ name: 'John', age: 25 \} 在JS中會有什麼樣的記憶體分配？ ->->-> `在這裡由於是擁有執行時會變更記憶體區塊大小需求的物件，所以會於heap 記憶體區塊儲存以下內容，並於stack記憶體建立一個區塊來儲存該物件在heap的記憶體位址，stack記憶體區塊會被命名為person  \{name: "John", age: 25\}。`

#🧠 JS：多個儲存物件內容的記憶體區塊傳遞方式為何？ ->->-> `由於識別字會是以stack記憶體區塊為主，所以會建立一個stack記憶體區塊來儲存另一個被複製過來的reference value，其值為對應heap記憶體位址。`


#🧠 JS：物件的記憶體區塊識別字是為何？又儲存在哪？->->-> `識別字會以專門儲存物件所在的heap記憶體位址的stack記憶體區塊為主，儲存在stack記憶體`

#🧠 當從另一個專門儲存object內容的變數A複製其值至另一個變數B時，JS引擎會以什麼區塊名稱來表示物件->->-> `以stack記憶體區塊名稱來表示，而stack記憶體區塊則是儲存對應物件的heap記憶體位址`

#🧠 當從另一個專門儲存object內容的變數A複製其值至另一個變數B時，JS引擎由於會以stack 記憶體區塊名稱來表示物件，過程會是？ ->->-> `	- 以reference value大小來製作一個固定大小的新stack記憶體區塊 - 接著把變數A的對應reference value複製至新stack記憶體區塊，並為記憶體區塊設定對應名稱為變數B`

#🧠 當從另一個專門儲存object內容的變數A複製其值至另一個變數B時，JS引擎由於會以stack 記憶體區塊名稱來表示物件，做完處理後，變數A和變數B的記憶體狀況是什麼？又可以做什麼？ ->->-> `- 在這裡變數A和變數B都會因為相同的reference value而指向相同的物件。這使得可透過變數A和變數B來調整相同的heap 記憶體區塊`

#🧠  JS的物件為何可以在執行時變更屬性名稱和屬性值 ->->-> `JS的物件本身定調為會在執行過程中變更其物件內容所佔取的記憶體區塊大小，也就是儲存在heap記憶體區塊`

#🧠 JS的primitive data value 可不可以在執行時變更其記憶體區塊 ->->-> `並不能，因為他們存放在不可改變大小的stack記憶體區塊`

#🧠 JS的primitive data value 可不可以在執行時像物件那樣隨意增加/移除/修改屬性  ->->-> `並不能，因為他們存放在不可改變大小的stack記憶體區塊`


#🧠 let name = 'John'; name.alias = 'Knight'; console.log(name.alias); JS執行起來會得到什麼？->->-> `由於name本身是stack記憶體區塊，本身無法在執行時增加屬性，所以會得到的值會是underfined`

#🧠 let person = \{ name: 'John', age: 25 \}; let member = person; 請問person 和 member兩者的記憶體狀況和使用是如何？ ->->-> `兩者會是儲存同個物件的heap記憶體位址，所以在使用上，兩個識別字會對應相同的heap記憶體`


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 的 primitive data value 和 reference value 本身並不會有執行過程會變更大小的需求，所以會存放於stack記憶體區塊，並用變數名稱作為其區塊的識別名稱]]
References:
[[@javascripttutorialJavaScriptPrimitiveVs]]