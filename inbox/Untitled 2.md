## 描述
[[@reactRefsHeDOM]]
> Ref 提供了一種可以取得 DOM 節點或在 render 方法內建立 React element 的方式。


> 在典型的 React 資料流裡，props 是 parent component 和 child component 唯一的互動方式。你會藉由使用新的 prop 重新 render 來改變你的 child。然而，有些情況下你需要在典型的資料流以外更改你的 child。這個被更改的 child 可能是 React component 的其中一個 instance，或他可能是個 DOM element。在這兩種情況下，React 提供了「逃生口」



> `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

useRef 回傳的是一個可變的object，該物件會擁有current這屬性，這屬性的初始值會依照下面的initialVlaue為主，其物件會跟著綁定元件，直到該元件的生命週期結束才被釋放其hook。
```
const something = useRef(initialValue)
```



> 什麼時候該使用 Ref

> 有幾種適合使用 ref 的情況：

> - 管理 focus、選擇文字、或影音播放。
> - 觸發即時的動畫。
> - 與第三方 DOM 函式庫整合。

### mutable object 命名緣由
[[@mdnMutableMDNWeb]]
> A **mutable object** is an object whose state can be modified after it is created.

mutable
> able or likely to change

重點：
- mutable 指的是可改變的
- 若一個物件被建立之後，物件內容還能夠被修改，該物件就是mutable object

### immutable object 命名緣由
[[@mdnMutableMDNWeb]]
> **Immutables** are the objects whose state cannot be changed once the object is created.

immutable 
> not changing, or unable to be changed


重點：
- immutable 指的是不能被改變的或者不變的
- 若一個物件被建立之後，物件內容不能夠被修改，該物件就是immutable object


## 複習

---
Status: #🌱 #📓 
Tags:
[[React]] 
Links:
References:
[[@reactRefsHeDOM]]
[[@mdnMutableMDNWeb]]