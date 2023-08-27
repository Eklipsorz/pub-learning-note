## 描述


### 用法
[[@ReactZhongDeForwardRefa]]
> ## React.forwardRef

> 对于ref转发，官网是这样描述的

> Ref 转发是一项将 [ref](https://link.juejin.cn?target=https%3A%2F%2Freact.docschina.org%2Fdocs%2Frefs-and-the-dom.html "https://react.docschina.org/docs/refs-and-the-dom.html") 自动地通过组件传递到其一子组件的技巧。对于大多数应用中的组件来说，这通常不是必需的。但其对某些组件，尤其是可重用的组件库是很有用的。

> 想详细了解的可以去看官方文档 [Refs 转发 – React (docschina.org)](https://link.juejin.cn?target=https%3A%2F%2Freact.docschina.org%2Fdocs%2Fforwarding-refs.html%23forwarding-refs-in-higher-order-components "https://react.docschina.org/docs/forwarding-refs.html#forwarding-refs-in-higher-order-components")

> 现在让我们直奔主题吧！

> `React.forwardRef(render)`的返回值是`react`组件，接收的参数是一个 `render`函数，函数签名为`render(props, ref)`，第二个参数将其接受的 [ref](https://link.juejin.cn?target=https%3A%2F%2Freact.docschina.org%2Fdocs%2Frefs-and-the-dom.html "https://react.docschina.org/docs/refs-and-the-dom.html") 属性**转发**到`render`返回的组件中。

> 这项技术并不常见，但在以下两种场景中特别有用:
> -   转发 `ref` 到组件内部的`DOM` 节点上



[[@reactForwardingRefsReact]]
> **Ref forwarding is an opt-in feature that lets some components take a `ref` they receive, and pass it further down (in other words, “forward” it) to a child.**

重點：
- forwardRef 是由React函式庫提供的方法之一，最主要是將目前Ref物件傳送至指定元件，由forwardRef函式接收到，並轉發至其指定元件所對應的component function 來處理，通常會有的處理會是：
	- forwardRef + useImperativeHandle ：讓指定元件a的Ref 物件設定為指定元件B內的部分對應DOM指令處理
	- 將目前元件的Ref 轉發至指定元件所對應的function來對應其child component的特定DOM節點。
	- 無關parent-child關係的元件間來進行轉發和ref對應

- 語法：在這裡會先由forwardRef接收到ref物件，然後再由他轉發至對應的component function
	- render 是指對應元件的render或者component function，其function會是(props, refs)，props會是該元件的屬性，refs則是接收到的ref物件
	-  forwardRef 回傳React Component，但這個Component 可被Ref技術擷取到對應的實際DOM節點
```
React.forwardRef(render)
```

細節：
	- refs 技術預設只支援原生HTML元件，不支援自製元件
	- 若自製元件想被支援，就使用forwardRef就能實現
### forwarding 命名緣由
> to send a letter, etc., especially from someone's old address to their new address, or to send a letter, email, etc. that you have received to someone else

重點：
- forward：將從特定事物A獲取的事物發送給其他事物B

## 複習

#🧠 forwardRef 語法在React框架會是隸屬於哪個函式庫 ->->-> `React`
<!--SR:!2023-11-23,134,246-->

#🧠 forwardRef 是React 函式庫的什麼？->->-> `是由React函式庫提供的方法之一`
<!--SR:!2024-12-05,493,250-->

#🧠 React：forwardRef 最主要是做什麼？ ->->-> `最主要是將目前Ref物件傳送至指定元件，由forwardRef函式接收到，並轉發至其指定元件所對應的component function 來處理`
<!--SR:!2024-01-04,163,230-->

#🧠 React：forwardRef 最主要是將目前Ref物件傳送至指定元件，由forwardRef函式接收到，並轉發至其指定元件所對應的component function 來處理，通常會有的處理會是什麼？ ->->-> `	forwardRef + useImperativeHandle ：讓指定元件a的Ref 物件設定為指定元件B內的部分對應DOM指令處理 - 將目前元件的Ref 轉發至指定元件所對應的function來對應其child component的特定DOM節點。 - 無關parent-child關係的元件間來進行轉發和ref對應`
<!--SR:!2023-11-08,166,210-->

#🧠 React：forwardRef 最主要是將目前Ref物件傳送至指定元件，由forwardRef函式接收到，並轉發至其指定元件所對應的component function 來處理，若搭配useImperativeHandle會是什麼？  ->->-> `forwardRef + useImperativeHandle ：讓指定元件a的Ref 物件設定為指定元件B內的部分對應DOM指令處理`
<!--SR:!2024-12-14,502,250-->

#🧠  React：forwardRef 語法形式->->-> `React.forwardRef(render)`
<!--SR:!2024-03-26,212,227-->


#🧠 React：forwardRef 語法形式的render是什麼？ ->->-> `render 是指對應元件的render或者component function，其function會是(props, refs)，props會是該元件的屬性，refs則是接收到的ref物件`
<!--SR:!2024-04-29,280,247-->

#🧠  React：forwardRef 語法形式回傳什麼 ->->-> `forwardRef 回傳React Component，但這個Component 可被Ref技術擷取到對應的實際DOM節點`
<!--SR:!2023-10-17,61,227-->

#🧠 React：若要讓元件A使用forwardRef將元件A的ref轉遞至元間B來處理，其概念要如何表示？請試著用程式碼來說明 ->->-> ``
<!--SR:!2024-04-19,276,247-->

#🧠 React： ref 技術支援所有元件嗎？->->-> `只有支援原生HTML元件`
<!--SR:!2024-12-04,492,250-->

#🧠 React： ref 技術支援自製元件嗎？如\<Componet \/\>->->-> `不支援`
<!--SR:!2024-11-09,474,250-->

#🧠 React： ref 技術不支援自製元件嗎？如\<Componet \/\>-> 若要支援的話，得用什麼技術？->-> `forwardRefs`

#🧠  forwarding 命名緣由 ->->-> `將從特定事物A獲取的事物發送給其他事物B`
<!--SR:!2024-11-22,480,250-->

#🧠 forwardRefs 對於 元件間和forward有什麼樣關聯會取名成forwardRefs->->-> ``
<!--SR:!2024-12-13,501,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useImperativeHandle 是定義一組以DOM原生渲染指令為主的處理來賦予至對應ref物件的current屬性]]
References:
[[@ReactZhongDeForwardRefa]]
[[@reactForwardingRefsReact]]