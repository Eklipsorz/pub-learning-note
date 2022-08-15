
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
- 對於標籤的屬性(attribute)事件綁定來說，React官方語法和HTML DOM官方語法都有各自的語法規則，兩者並不互通：
	- 當使用React 官方語法來建立事件綁定，並不會轉換成以HTML DOM來綁定，而是以JS來綁定
	- 當使用HTML DOM官方語法來建立事件綁定，由於React是基於HTML而產生的應用框架，本身底層不會影響到React
- 標籤的屬性(attribute)事件綁定語法：
	- React：屬性名稱形式會是onXXXX，XXXX會是指事件名稱，該屬性名稱則以lower camel case為主，如負責點擊事件綁定的onClick
	```
	<button onClick={activateLasers}>  
		Activate Lasers
	</button>
	```
	- HTML DOM： 屬性名稱形式會是onXXXX，XXXX會是指事件名稱，名稱則都是以小寫為主，因得考慮支援XHTML，如負責點擊事件綁定的onclick
	```
	<button onclick="activateLasers()">
		Activate Lasers
	</button>
	```
- 事件綁定的事件處理函式指派：
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

#🧠 對於標籤上的屬性(attribute)事件綁定來說，React 官方語法和HTML DOM 官方語法之間是否有關係？獨立？相依？->->-> `兩者都有各自的語法規則，兩者並不互通`


#🧠 對於標籤上的屬性(attribute)事件綁定來說，React 官方語法和HTML DOM 官方語法之間是獨立，請試著以React官方語法角度和HTML DOM角度來說明 ->->-> `當使用React 官方語法來建立事件綁定，並不會轉換成以HTML DOM來綁定，而是以JS來綁定；當使用HTML DOM官方語法來建立事件綁定，由於React是基於HTML而產生的應用框架，本身底層不會影響到React`

#🧠 標籤的屬性(attribute)事件綁定語法，React會是用何種形式 ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[inline javascript 是指會在HTML文件內部加入JavaScript語法的開發方式，而onclick=function()則是指定事件發生時要執行的指令]]
References:
[[@reactShiJianChuLiReact]]