## 描述
### React element


[[@facebookRenderElementReact]] 所描述

> 建立 React 應用程式最小的單位是 element。
> 一個 element 描述你想要在螢幕上所看到的：

```
const element = <h1>Hello, world</h1>;
```

> 與瀏覽器的 DOM element 不同，React element 是單純的 object，而且很容易被建立。React DOM 負責更新 DOM 來符合 React element。

重點：React element
1. 是建立React 應用程式最小的建立單位
2. 相當於Virtual DOM節點
3. 語法形式為：使用XML表示
```
<tag1>content</tag1>
```


### 使用function 定義component
> 定義 component 最簡單的方法即是撰寫一個 Javascript function：

```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

> 此 function 是一個符合規範的 React component，因為它接受一個「props」（指屬性 properties）物件並回傳一個 React element。我們稱之為 function component，因為它本身就是一個 JavaScript function。

重點：
- 如何用function來定義component：function ＋ 回傳 React element 
- 使用function 來定義的component，稱之為function component

### 使用class 定義component


> 同樣的，你也可以使用 [ES6 Class](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes) 來定義 component：

```
// Your code  
class Greeting extends React.Component {  
  render() {  
    return <p>Hello</p>;  
  }  
}// Inside React  
const instance = new Greeting(props); // Greeting {}  
const result = instance.render(); // <p>Hello</p>
```

> 上述兩種 component 在 React 中是同等的。

> Function 和 Class component 兩者都擁有額外的特性，我們將會在[下一個章節](https://zh-hant.reactjs.org/docs/state-and-lifecycle.html)探討。


重點：
- 利用class的話，實際上是利用建構式來建構出prototype，並且利用new按照prototype來建立實例，最後由實例呼叫對應render來得到對應react element

## 複習

#🧠 構建React 應用程式的最小單位是什麼？ ->->-> `React element`
<!--SR:!2023-11-27,287,250-->

#🧠 React element 語法形式是什麼？ ->->-> `以XML語法為主`
<!--SR:!2023-06-14,193,250-->

#🧠 每一個React element 在 JS 語言體系下會是甚麼?->->-> `相當於Virtual DOM物件`
<!--SR:!2024-04-12,369,250-->

#🧠 (重複)每一個React element 在 JS 語言體系下會是甚麼?->->-> `相當於Virtual DOM物件`
<!--SR:!2023-10-06,32,230-->


#🧠 React：如何構建一個function component? ->->-> `使用function以及function回傳著react element構成的元件`
<!--SR:!2024-11-09,498,250-->

#🧠 React：如何構建component?  ->->-> `使用function或者class`
<!--SR:!2023-05-26,179,250-->

#🧠 React：使用function來構建的component 稱之為什麼 ->->-> `function component`
<!--SR:!2023-06-05,186,250-->

#🧠 React： 使用class來建立component，具體會是什麼？ ->->-> `利用class的話，實際上是利用建構式來建構出prototype，並且利用new按照prototype來建立實例，最後由實例呼叫對應render來得到對應react element`
<!--SR:!2023-10-06,255,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@facebookComponentsYuProps]]
[[@facebookRenderElementReact]]