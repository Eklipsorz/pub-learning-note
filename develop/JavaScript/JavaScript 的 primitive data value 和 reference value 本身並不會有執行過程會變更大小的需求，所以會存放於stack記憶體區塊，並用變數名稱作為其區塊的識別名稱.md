## 描述


### primitive data type

[[@javascripttutorialJavaScriptPrimitiveVs]]
> When you declare variables, the JavaScript engine allocates the memory for them on two memory locations: stack and heap.

> Static data is the data whose size is fixed at compile time. Static data includes:
> - Primitive values (null, undefined, boolean, number, string, symbol, and BigInt)
> - Reference values that refer to objects.


> Because static data has a size that does not change, the JavaScript engine allocates a fixed amount of memory space to the static data and store it on the stack.


> Note that strings are objects in many programming languages, including Java and C#. However, strings are primitive values in JavaScript.


NaN
[[@mdnInstanceofJavaScriptMDN]]
> The global **`NaN`** property is a value representing Not-A-Number.
> `NaN` is a property of the _global object_. In other words, it is a variable in global scope.


[[@javascript.infoDataTypes]]
> Besides regular numbers, there are so-called “special numeric values” which also belong to this data type: `Infinity`, `-Infinity` and `NaN`.

重點：
- 當在JS程式碼宣告變數時，主要會分配兩種記憶體區塊種類：
	- stack 記憶體區塊：專門儲存著固定大小的資料
	- heap 記憶體區塊：專門儲存著會於執行時調整大小的資料
- JS變數儲存的Primitive data type 或者 Reference value  (對應其物件的記憶體位址)：
	- 在編譯時就確定其資料大小 
	- 執行過程中並不會調整其資料所存放的記憶體區塊大小，即確定後大小就固定大小不動
- JS 的Primitive data type 會是 null、undefined、boolean、number、string、symbol、BigInt，其中string 在其他語言並不會是primitive data type
- NaN(Not-A-Number) 是算primitive data type中的number，只是它被當作評斷特定內容是否為非數字的特殊數字型別
### Storing Values



```javascript
let name = 'John';
let age = 25;
```
> Because `name` and `age` are primitive values, the JavaScript engine stores these variables on the stack as shown in the following picture:

![](https://www.javascripttutorial.net/wp-content/uploads/2022/01/JavaScript-stack-memory.svg)


重點：
- primitive data value 以及 reference value 會因為本身並不會在執行過程改變記憶體區塊大小而直接存放在專門儲存固定大小的stack記憶體區塊
- 系統會為 儲存primitive data value 或者 reference value的記憶體區塊 設定對應名稱或者識別名稱，該名稱會是變數名稱
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

重點：
- 多個儲存primitive data value 或者 reference value的記憶體區塊傳遞方式：建立另一個記憶體區塊並儲存複製過來的值
- 當從另一個專門儲存primitive data value的變數A複製其值至另一個變數B時，JS引擎會
	- 依據primitive data value的大小來製作一個固定大小的新記憶體區塊
	- 接著把變數A的對應primitive data value複製至新記憶體區塊，並為記憶體區塊設定對應名稱為變數B
- 從另一個專門儲存primitive data value的變數A複製其值至另一個變數B 語法會是
	- variableA 會是指專門儲存primitive data value的stack記憶體區塊，該區塊的名稱為variableA
	- variableB 會是指專門接收並儲存variableB的stack記憶體區塊，記憶體區塊，該區塊的名稱為variableB
```
variableA = variableB
```



#### 案例：

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


重點：
- 在這裡先分配一個固定大小的stack記憶體區塊來存放25這值，其區塊的對應名稱為age
- 接著由於下面語法，是要複製age對應的記憶體內容至另一個stack記憶體區塊，所以會特意建立一個記憶體區塊且名為newAge，其內容會是25。
```
let newAge = age;
```
- 接著由於age和newAge本身是兩個獨立記憶體區塊，所以僅會針對newAge所儲存的內容進行+1，age內容並不會有任何變化。
```
newAge = newAge + 1;
console.log(age, newAge);
```

## 複習

#🧠 當在JS程式碼宣告變數時，主要會分配兩種記憶體區塊種類？ ->->-> `stack 記憶體區塊、heap 記憶體區塊種類`
<!--SR:!2024-03-19,320,250-->

#🧠 當在JS程式碼宣告變數時，主要會分配兩種記憶體區塊種類？stack 記憶體區塊是專門儲存什麼？->->-> `專門儲存著固定大小的資料`
<!--SR:!2024-09-14,424,250-->


#🧠 當在JS程式碼宣告變數時，主要會分配兩種記憶體區塊種類？heap 記憶體區塊是專門儲存什麼？ ->->-> `專門儲存著會於執行時調整大小的資料`
<!--SR:!2023-09-30,79,230-->


#🧠 JS變數儲存的Primitive data type 或者 Reference value  (對應其物件的記憶體位址)，其儲存資料的記憶體會擁有什麼特性？ ->->-> `- 在編譯時就確定其資料大小  - 執行過程中並不會調整其資料所存放的記憶體區塊大小，即確定後大小就固定大小不動`
<!--SR:!2023-09-09,208,249-->

#🧠 JS的primitive data type 會有什麼？ ->->-> `null、undefined、boolean、number、string、symbol、BigInt`
<!--SR:!2023-09-01,15,130-->


#🧠 NaN是屬於primitive data type嗎？為什麼？ ->->-> `NaN 是算primitive data type中的number`
<!--SR:!2023-12-06,141,228-->

#🧠 NaN 是算primitive data type中的number，它的用途是什麼？ ->->-> `當作評斷特定內容是否為非數字的特殊數字型別`
<!--SR:!2024-01-28,265,248-->

#🧠 NaN 是算primitive data type中的number，請問NaN的全名是什麼？->->-> `Not-A-Number`
<!--SR:!2024-03-20,301,248-->

#🧠 primitive data value 以及 reference value 會存放在哪種記憶體區塊？stack ? heap? 為什麼？->->-> `因為本身並不會在執行過程改變記憶體區塊大小而直接存放在專門儲存固定大小的stack記憶體區塊`
<!--SR:!2023-10-24,231,249-->

#🧠 程式語言要如何獲取 儲存對應primitive data value 或者對應 reference value的記憶體區塊  ->->-> `具體會為記憶體區塊取特定識別名稱或者變數名稱，來指定特定區塊`
<!--SR:!2024-04-03,260,230-->

#🧠 let name = 'John'; 在JS中會是代表什麼？（請說明名稱和內容) ->->-> ` 會分配一個固定大小的區塊來存放John，並為記憶體區塊設定對應名稱為name`
<!--SR:!2024-12-24,499,249-->

#🧠 let age = 25; 在JS中會是代表什麼？（請說明名稱和內容)  ->->-> `會分配一個固定大小的區塊來存放25，並為記憶體區塊設定對應名稱為age`
<!--SR:!2023-12-14,106,229-->

#🧠 當從另一個專門儲存primitive data value的變數A複製其值至另一個變數B時，JS引擎會做什麼？ ->->-> `	- 依據primitive data value的大小來製作一個固定大小的新記憶體區塊 - 接著把變數A的對應primitive data value複製至新記憶體區塊，並為記憶體區塊設定對應名稱為變數B`
<!--SR:!2024-09-20,430,250-->

#🧠 當從另一個專門儲存primitive data value的變數A複製其值至另一個變數B時，JS引擎做完特定處理後，記憶體會發生什麼？ ->->-> `會有兩個獨立的記憶體區塊，第一個區塊名稱是變數A，第二個區塊名稱是變數B，儲存著從變數A對應的記憶體內容。`
<!--SR:!2024-11-10,468,250-->

#🧠  JS ：多個儲存primitive data value 或者 reference value的記憶體區塊傳遞方式->->-> `建立另一個記憶體區塊並儲存複製過來的值`
<!--SR:!2023-12-05,257,249-->

#🧠 JS ：儲存primitive data value 和 reference value的記憶體區塊傳遞方式，其語法會是什麼？ ->->-> `variableA = variableB`
<!--SR:!2024-08-25,411,250-->

#🧠 JS ：儲存primitive data value 和 reference value的記憶體區塊傳遞方式，其語法會是variableA = variableB，那麼這在系統解析上會是什麼？ ->->-> `	- variableA 會是指專門儲存primitive data value的stack記憶體區塊，該區塊的名稱為variableA - variableB 會是指專門接收並儲存variableB的stack記憶體區塊，記憶體區塊，該區塊的名稱為variableB`
<!--SR:!2024-09-08,421,250-->


#🧠 JS ：儲存primitive data value 和 reference value的記憶體區塊傳遞方式，其語法會是variableA = variableB，那麼一旦他們做完，兩者內容之間的關係為何 ->->-> `兩者所存的內容皆為獨立，互不影響。`
<!--SR:!2024-07-26,337,247-->


#🧠 let age = 25; let newAge = age; newAge = newAge + 1; 在JS中的記憶體處理會是如何？請說明 ->->-> `- 在這裡先分配一個固定大小的stack記憶體區塊來存放25這值，其區塊的對應名稱為age - 接著由於下面語法，是要複製age對應的記憶體內容至另一個stack記憶體區塊，所以會特意建立一個記憶體區塊且名為newAge，其內容會是25。 - 接著由於age和newAge本身是兩個獨立記憶體區塊，所以僅會針對newAge所儲存的內容進行+1，age內容並不會有任何變化。`
<!--SR:!2024-03-26,323,250-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[primitive data type 是指 電腦環境本身帶有的資料型別，而非程式語言會衍生的，該型別可以在程式語言下，組合成新的資料型別，如物件]]
References:
[[@javascripttutorialJavaScriptPrimitiveVs]]
[[@mdnInstanceofJavaScriptMDN]]
[[@javascript.infoDataTypes]]