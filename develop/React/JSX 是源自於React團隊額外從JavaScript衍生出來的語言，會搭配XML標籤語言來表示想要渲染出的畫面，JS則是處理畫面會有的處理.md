
## 描述


### JSX 起源
JSX 全名為JavaScript XML
1. 是由React團隊額外從JavaScript衍生出來的語言，會搭配XML標籤語言來表示想要渲染出的畫面
2. JSX 整體的開發邏輯是將UI渲染部分和UI上會有的處理(含事件處理)綁在一塊成為一個component，並以component作為模組來給予他人使用：
	- XML 表示UI渲染部分，由開發者來告知系統渲染目標為何，另外以state作為渲染目標
	- JavaScript 表示UI會有的處理

[[@facebookJieShaoJSXReact]] 所描述
> React 擁抱了 render 邏輯從根本上就得跟其他 UI 邏輯綁在一起的事實：事件要怎麼處理？隨著時間經過 state 會如何變化？以及要怎麼將資料準備好用於顯示？

> 與其刻意的將_技術_拆開，把標籤語法跟邏輯拆放於不同檔案之中，React [_關注點分離_](https://en.wikipedia.org/wiki/Separation_of_concerns)的方法是將其拆分為很多同時包含 UI 與邏輯的 component，而彼此之間很少互相依賴。

3. JSX 本身不被瀏覽器解讀，必須經過Babel 轉譯成 對應的JavaScript



#### JSX 使用XML 是為了  
1. 方便讓人類解讀渲染部分  
2. HTML本身也支援著XML，轉換的話，也只需要花較少的成本

### JSX 會有的語法


#### 用function來表達component
[[React - 可使用function 和 class 來建構react component]]
```
function App() {
    return (
         <div>
             <h2> ....</h2>
        </div>
   );
}
```

1. It's also not valid JavaScript code normally
2. This is JSX


#### 識別字指向特定React DOM
```
<App />
```

<App />：
1. that is definitely not regular JavaScript syntax here
2. This is a syntax called JSX
3. It means React component

在這裡App識別字會指向於構建特定React DOM的函式物件或者由class所構建的component

  
#### JSX 支援CSS-in-JS

```
import './index.css';
```




## 複習
#🧠 JSX 全名是什麼語言？ ->->-> `JavaScript XML`
<!--SR:!2022-10-25,47,250-->

#🧠 JSX 語言是什麼？ ->->-> `是由React團隊額外從JavaScript衍生出來的語言，會搭配XML標籤語言來表示想要渲染出的畫面`
<!--SR:!2022-09-20,28,250-->

#🧠 JSX 語言的開發邏輯是？ ->->-> `JSX 整體的開發邏輯是將UI渲染部分和UI上會有的處理(含事件處理)綁在一塊成為一個component，並以component作為模組來給予他人使用`
<!--SR:!2022-11-13,59,250-->

#🧠 JSX 使用XML 是為了什麼？ ->->-> `方便讓人類解讀渲染部分、HTML本身也支援著XML，轉換的話，也只需要花較少的成本`
<!--SR:!2022-09-20,28,250-->

#🧠 JSX能被瀏覽器解讀嗎？ ->->-> `不能`
<!--SR:!2022-09-20,28,250-->

#🧠 JSX不能被瀏覽器解讀，那麼如何做，才能使瀏覽器解讀？->->-> `必須經過Babel 轉譯成 對應的JavaScript`
<!--SR:!2022-09-17,26,250-->

#🧠 JSX 和 JS有何關係 ->->-> `JSX是延伸JS的語法來做為React 的語法糖`
<!--SR:!2022-09-21,11,230-->



---
Status: #🌱 
Tags:
[[React]] - [[HTML]]
Links:
[[SGML 是標準標籤語言，以這語言為基底來打造出HTML，隨後以精簡SGML的形式來推出XML，並讓XML去支援HTML所欠缺的不足]]
[[React - 可使用function 和 class 來建構react component]]
References:
[[@facebookJieShaoJSXReact]]