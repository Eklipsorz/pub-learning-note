
## 描述
[[@reactShiJianChuLiReact]]
> 使用 React element 處理事件跟使用 DOM element 處理事件是十分相似的。它們有一些語法上的差異：
> -   事件的名稱在 React 中都是 camelCase，而在 HTML DOM 中則是小寫。
> -   事件的值在 JSX 中是一個 function，而在 HTML DOM 中則是一個 string。


> 例如，在 HTML 中的語法：
```
<button onclick="activateLasers()">
	Activate Lasers
</button>
```

> 和在 React 中的語法有些微的不同：
```
<button onClick={activateLasers}>  
	Activate Lasers
</button>
```


JSX 為React Element提供事件綁定的API：
- 在指定元件的標籤上添加onXXXX屬性，後面接著function，XXXX 會是指事件名稱
- 這裡的onXXXX是react官方提供的語法
- 且轉換後的語法，也並不會實際直接以HTML方式來定義onClick，而是以JS來綁定



重點：
- 對於標籤的屬性(attribute)事件綁定來說，React官方語法和HTML DOM官方語法都有各自的用法規則，兩者並不互通：
	- React 事件綁定 本身定義著函式本身和定義其內容；HTML DOM則只是定義好函式本身，只是等開發者設定指令來為函式定義內容
- 標籤的屬性(attribute)事件綁定語法：
	- React：屬性名稱形式會是onXXXX，XXXX會是指事件名稱，該屬性名稱則以lower camel case為主，如負責點擊事件綁定的onClick
	```
	<button onClick={activateLasers}>  
		Activate Lasers
	</button>
	```
	- HTML DOM： 屬性名稱形式會是onXXXX，XXXX會是指事件名稱，名稱則都是以小寫為主，因得考慮支援XHTML、XML，如負責點擊事件綁定的onclick
	```
	<button onclick="activateLasers()">
		Activate Lasers
	</button>
	```
- 屬性(attribute)事件綁定的事件處理函式指派：
	- React：指派函式則是以函式物件為主，不用特別添加()，如下的activateLasers函式物件。
	```
	onClick={activateLasers}
	```
	- HTML：指派函式則是以字串來表示來表示事件發生時要執行什麼樣的指令
	```
	onclick="activateLasers()"
	```


### onClick 夾雜的函式是否呼叫

```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler}></button>
)
```

若在JSX 語法中來呼叫clickHandler，會直接先執行clickHandler，並拿它回傳的內容來替代呼叫clickHandler，最後以那個內容來渲染。
```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler()}></button>
)
```


### 命名每個事件綁定的callback
```
function clickHandler(...) {
	....
}

// JSX Code
(
	<button onClick={clickHandler()}></button>
)
```


若沒特別命名法則來命名每個事件綁定的callback，那麼可以試著以 xxxx + Handler 來命名，其中xxxx為事件名稱。
```
const clickHandler = () => {
	.....
}
```

畢竟clickHandler最後會是由瀏覽器自己去幫忙執行，而非由React本身來處理


## 複習

#🧠 對於標籤上的屬性(attribute)事件綁定來說，React 事件綁定和HTML DOM 上事件綁定之間是否有關係？獨立？相依？->->-> `無關，React 事件綁定 本身定義著函式本身和定義其內容；HTML DOM則只是定義好函式本身，只是等開發者設定指令來為函式定義內容`
<!--SR:!2024-06-09,294,227-->



#🧠 標籤的屬性(attribute)事件綁定語法，React會是用何種形式來表示 ->->-> `onXXXX，，XXXX會是指事件名稱，該屬性名稱則以lower camel case為主`
<!--SR:!2023-10-02,213,210-->

#🧠 標籤的屬性(attribute)事件綁定語法，React會是用何種形式來表示，舉一個點擊事件的例子->->-> `onClick`
<!--SR:!2024-01-16,312,250-->

#🧠 標籤的屬性(attribute)事件綁定語法，HTML DOM會是何種形式來表示？ ->->-> `屬性名稱形式會是onXXXX，XXXX會是指事件名稱，名稱則都是以小寫為主`
<!--SR:!2024-11-03,495,250-->

#🧠 標籤的屬性(attribute)事件綁定語法，HTML DOM上為何是以小寫來表示？->->-> `因得考慮支援XHTML、XML`
<!--SR:!2025-02-27,562,250-->

#🧠 標籤的屬性(attribute)事件綁定語法，HTML DOM會是用何種形式來表示，舉一個點擊事件的例子 ->->-> `onclick`
<!--SR:!2025-03-18,569,250-->

#🧠 屬性(attribute)事件綁定的事件處理函式指派，React是如何指派的？ ->->-> `指派函式則是以函式物件為主`
<!--SR:!2024-01-29,321,250-->

#🧠 屬性(attribute)事件綁定的事件處理函式指派，React會是用何種形式來指派 ->->-> `onXXXX={function}，其中function是函式物件`
<!--SR:!2024-07-07,419,250-->

#🧠 屬性(attribute)事件綁定的事件處理函式指派，HTML會是用何種形式來指派 ->->-> `onXXXX="function();"，HTML是指定事件發生時要執行什麼指令，在這裡就直接指定執行function就好，也就是function()，同時並用字串符號來包覆`
<!--SR:!2023-05-21,162,230-->

#🧠 屬性(attribute)事件綁定的事件處理函式指派，React是指派函式物件來指定對應事件處理，那麼要先需要添加()來先呼叫？若添加會發生什麼？？->->-> `不用特別添加()，若添加就等同於先執行函式，並以函式處理結果來替代整個函式呼叫的所在，最後以這內容作為渲染內容`
<!--SR:!2024-06-20,409,250-->


#🧠  使用React element 來設定處理事件跟使用 DOM element 來設定處理事件是十分相似的。他們有差異有哪些？ (語法)->->-> `語法：1. 事件綁定屬性的名稱在React上是以lowerCamel；事件綁定屬性的名稱在HTML DOM上面是以小寫 2. 事件綁定屬性的對應值在React是以一個函式物件來表示；事件綁定屬性的對應值在HTML DOM是以字串指令來表示，其指令是直接下達事件發生時要執行什麼。`
<!--SR:!2023-11-26,101,230-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[inline javascript 是指會在HTML文件內部加入JavaScript語法的開發方式，而onclick=function()則是指定事件發生時要執行的指令]]
References:
[[@reactShiJianChuLiReact]]