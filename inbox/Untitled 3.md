## 描述


### primitive data type

[[@javascripttutorialJavaScriptPrimitiveVs]]
> When you declare variables, the JavaScript engine allocates the memory for them on two memory locations: stack and heap.

> Static data is the data whose size is fixed at compile time. Static data includes:
> - Primitive values (null, undefined, boolean, number, string, symbol, and BigInt)
> - Reference values that refer to objects.


> Because static data has a size that does not change, the JavaScript engine allocates a fixed amount of memory space to the static data and store it on the stack.


> Note that strings are objects in many programming languages, including Java and C#. However, strings are primitive values in JavaScript.

重點：
- 當在JS程式碼宣告變數時，主要會分配兩種記憶體種類：
	- stack 記憶體區塊：專門儲存著固定大小的資料
	- heap 記憶體區塊：專門儲存著會於執行調整大小的資料
- JS變數儲存的靜態資料會是指：
	- 在編譯時就確定其資料大小 
	- 執行過程中並不會調整其資料所存放的記憶體區塊大小，即確定後大小就固定大小不動
	- 該資料會是Primitive data type 或者 Reference value (對應其物件的記憶體位址)
- JS 的Primitive data type 會是 null、undefined、boolean、number、string、symbol、BigInt，其中string 在其他語言並不會是primitive data type

### Storing Values



```javascript
let name = 'John';
let age = 25;
```
> Because `name` and `age` are primitive values, the JavaScript engine stores these variables on the stack as shown in the following picture:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-stack-memory.svg)


重點：
- primitive data type 以及 reference value 會因為本身並不會在執行過程改變記憶體區塊大小而直接存放在專門儲存固定大小的stack記憶體區塊
- 假若儲存以下內容：
	- 會分配一個固定大小的區塊來存放John，並為記憶體區塊設定對應名稱為name
	- 會分配一個固定大小的區塊來存放25，並為記憶體區塊設定對應名稱為age
```
let name = 'John';
let age = 25;
```



### Copying values
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
[[JavaScript]]
Links:
[[primitive data type 是指 電腦環境本身帶有的資料型別，而非程式語言會衍生的，該型別可以在程式語言下，組合成新的資料型別，如物件]]
References:
[[@javascripttutorialJavaScriptPrimitiveVs]]