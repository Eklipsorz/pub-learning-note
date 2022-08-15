	
## 描述


```
function ExpenseItem(props) {
	let title = props.title;

    const clickHandler = () => {
		title = 'updated';
    };

    return (
  	<Card className='expense-item' id={props.id}>	
  		<ExpenseDate date={props.date} />
  		<div className='expense-item__description'>
  			<h2>{title}</h2>
  			<div className='expense-item__price'>{props.amount}</div>
  		</div>
  		<button onClick={clickHandler}>test btn</button>
  	</Card>
    );
}
```
  

在這裡按鈕綁定點擊事件的事件處理clickHandler，並且預期是透過點擊事件來變更title的內容，但結果是-點擊後毫無反應

這是因為
1. 預設上只有使用對應元件的標籤，才會渲染一次初步畫面，接著就不會做任何重複渲染
2. title 是有變更，只是變更時機都是發生在初步畫面的渲染之後，且預設上不會有任何重複渲染，所以也就沒重新渲染成title內容被變更後的畫面



先在其他元件上指定以下標籤就呼叫首次的對應函式，並透過函式的執行結果來渲染對應元件的樣貌和邏輯
```
<ExpenseItem></ExpenseItem>
```

### 解法：title 是有變更了，只是沒重新渲染成title內容被變更後的畫面

一旦呼叫就只會執行一次對應的函式，並不會重複執行

`<ExpenseItem></ExpenseItem>`

所以即使以事件觸發來修改對應函式裡頭的內容，但它不會重複執行，也就不會再次渲染。

解法1：
1. 透過事件處理來擷取該節點，並更改其內容

解法2：
1. 先更改內容
2. 然後以內容更改後的畫面來渲染

### 元件上的對應函式之初始呼叫

當以這形式來表示ExpenseItem元件時，就是呼叫ExpenseItem元件對應的函式，並執行函式內容和會回傳對應元件畫面

`<ExpenseItem></ExpenseItem>`

該函式會回傳以下JSX的對應渲染畫面
```
1.    return (
2.      <Card className='expense-item' id={props.id}>
3.        <ExpenseDate date={props.date} />
4.        <div className='expense-item__description'>
5.          <h2>{title}</h2>
6.          <div className='expense-item__price'>{props.amount}</div>
7.        </div>
8.        <button onClick={clickHandler}>test btn</button>
9.      </Card>
10.    );
```


接著當JSX回傳的對應渲染畫面還有擁有對應函式的自製元件，就會按照順序呼叫對應函式來執行並回傳對應畫面來與目前畫面結合，直到畫面能夠被確定：

1. 所有自製元件上的對應函式執行完畢
2. 所有DOM節點都被解析

  
拿以上為例子的話，確定畫面流程會是：
1. 先把Card這元件的對應函式呼叫並讓其回傳畫面至這來與目前畫面合併
2. 接著遇到ExpenseDate就以它對應函式來呼叫來讓其回傳畫面至這來與目前畫面合併
3. 剩下都是HTML原生元件，直接與目前畫面合併
  
接著確定畫面為何之後，就會以畫面為主來生成實際DOM節點的指令，透過執行指令來渲染畫面

  
畫面生成的整體流程會是：

確定畫面->轉換成以畫面為主來生成實際DOM節點的指令->執行指令來渲染，確定畫面則是則會有自製元件和原生元件，自製元件就直接執行對應的函式來獲取對應原生元件來合併，原生元件就直接合併

### 總結
1. 每個元件上都綁定著能夠渲染其元件樣貌和邏輯的函式
2. 函式何時呼叫：
	- 當調用對應元件就會做一次呼叫來當作最一開始的畫面渲染
	```
	<Component></Component>
	```
## 複習


#🧠 在這裡按鈕綁定點擊事件的事件處理clickHandler，並且預期是透過點擊事件來變更title的內容，結果能實現嗎？ 為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660567783/blog/react/event/wrong-example-event-handler_wu8fha.png) ->->-> `結果是點擊後毫無反應，這是因為1. 預設上只有使用對應元件的標籤，才會渲染一次初步畫面，接著就不會做任何重複渲染 2. title 是有變更，只是變更時機都是發生在初步畫面的渲染之後，且預設上不會有任何重複渲染，所以也就沒重新渲染成title內容被變更後的畫面`


#🧠 在這裡按鈕綁定點擊事件的事件處理clickHandler，並且預期是透過點擊事件來變更title的內容，結果是不能實現，請問有何解法？ (概念) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660567783/blog/react/event/wrong-example-event-handler_wu8fha.png) ->->-> `解法1： 透過事件處理來擷取該節點，並更改其內容、解法2：先更改內容，然後以內容更改後的畫面來渲染`

#🧠 在React裡，每個元件都實際綁定著什麼？ ->->-> `能夠渲染其元件樣貌和邏輯的函式`

#🧠 在React裡，每個元件的對應函式預設何時會呼叫？->->-> `當調用對應元件就會做一次呼叫來當作最一開始的畫面渲染，如<Component></Component>，就會呼叫Component 對應函式`


#🧠 React：以這個作為例子來說明，系統會如何執行、合併畫面、獲得畫面？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660567783/blog/react/event/wrong-example-event-handler_wu8fha.png) ->->-> `當以這形式來表示ExpenseItem元件時，<ExpenseItem></ExpenseItem>，就是呼叫ExpenseItem元件對應的函式，並執行函式內容和會回傳對應元件畫面，而畫面則是會以return()內容為主，在這裡會有Card和ExpenseDate這兩個自製元件，在這裡會直接執行他們對應的函式來獲取對應畫面來與目前畫面做合併，而剩下非自製則是直接與目前畫面做合併，直到畫面能夠被確定，才會生成實際DOM節點的指令，並透過指令來實際渲染畫面`

#🧠 React：以這個作為例子來說明，畫面生成的整體流程會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660567783/blog/react/event/wrong-example-event-handler_wu8fha.png) ->->-> `確定畫面->轉換成以畫面為主來生成實際DOM節點的指令->執行指令來渲染`

#🧠 React：是如何從return () 確定畫面的 ->->-> `確定畫面則是則會有自製元件和原生元件，自製元件就直接執行對應的函式來獲取對應原生元件來合併，原生元件就直接合併`



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: