## 描述
[[@reactRefsHeDOM]]
> Ref 提供了一種可以取得 DOM 節點或在 render 方法內建立 React element 的方式。


> 在典型的 React 資料流裡，props 是 parent component 和 child component 唯一的互動方式。你會藉由使用新的 prop 重新 render 來改變你的 child。然而，有些情況下你需要在典型的資料流以外更改你的 child。這個被更改的 child 可能是 React component 的其中一個 instance，或他可能是個 DOM element。在這兩種情況下，React 提供了「逃生口」



> `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

useRef 回傳的是一個可變的object，該物件會擁有current這屬性，這屬性的初始值會依照下面的initialVlaue為主，其物件會跟著綁定元件，直到該元件的生命週期結束才被釋放其hook。
```
const something = useRef(initialValue)
```

重點：
- useRef 是一種hook，綁定於特定元件下，其存活時間會和特定元件一起共存，直到生命週期結束才被釋放其hook
- useRef 主要是建立一個物件來參照特定實際DOM節點，以此讓目前元件來操作實際DOM節點
- useRef 函式本身會回傳一個mutable 物件，裡面夾雜了current屬性，其屬性值為對應參照的實際DOM節點

### 使用方法

with refs, we can set up a connection between a HTML element which is being rendered in the end and our other JS code

1. 首先要先從react函式庫載入useRefs函式
```
import { useRefs } from 'react';
```

2. 接著在對應的function component，使用useRefs來註冊hook至目前的元件：
	- useRef會產生一個夾雜current屬性的物件，其current屬性值初始值為initialValue
```
const ref1 = useRef(initialValue)
```

3. 在要參照的JSX元素綁定ref屬性，以此獲取JSX的對應實際DOM節點
```
<Element1 ref={ref1} />
```

#### 讀取
4. 若要讀取該JSX元素的對應DOM節點的話，可以使用
```
// 代表著Element1的對應實際DOM節點
ref1.current
```

#### 寫入
4. 若要修改該JSX元素的對應DOM節點所擁有的屬性的話，可以使用
```
// 對著實際DOM節點的屬性增加內容
ref1.current.xxxx = xxxx1
```


#### 使用案例1
使用方法為：

1. 從react函式庫調用名為useRef的hook來綁定目前元件

1.  // 回傳兩個物件，其current屬性值皆因為useRef沒給任何初始值而變成為undefined
2.  const nameInputRef = useRef()
3.  const ageInputRef = useRef()

  

2. 對想要進行連接的DOM節點

`<Element1 ref={nameInputRef} />`

  

3. 其nameInputRef會透過ref技術來擷取對應Element1的對應實際DOM節點

  

在對應DOM節點標籤上增加ref屬性

  

e.g.,

useRef and input which allow us to enter a username

useRef and input which allow us to enter a age

  

  

該Ref 技術可以綁定任何Virtual DOM和任何實際DOM
#### 使用案例2


reading value:
```
  // 回傳兩個物件，其current屬性值皆因為useRef沒給任何初始值而變成為undefined
  const nameInputRef = useRef()
  const ageInputRef = useRef()

  const submitHandler = (event) => {
      event.preventDefault()
      // current -> the real dom of input for nmae
      console.log(nameInputRef.current.value)
  }
```

```
  return (
      <form onSubmit={submitHandler}>
          <input ref={nameInputRef}> </input>
      </form>
  );
```

writing value:
```
nameInputRef.current.value = ''
```



> now, it's recommended that you don't manipulate it.
> Your DOM should really only be manipulated by React



> 什麼時候該使用 Ref

> 有幾種適合使用 ref 的情況：

> - 管理 focus、選擇文字、或影音播放。
> - 觸發即時的動畫。
> - 與第三方 DOM 函式庫整合。


rarely use refs to manipulate the DOM.

Here we're not really manipulating the DOM, we're not adding a new element.

  

use refs to manipulate the DOM ：

1. 只是改變如何取得狀態



You will sometimes have use cases where you just want to quickly read a value

and if you only want to read a value and you never plan on changing anything, well, then you don't really need state. because just to state as a keylogger is not that great. It's a lot of unnecessary code and work. 

  

so if you just want to read a value, refs are probably better.

  
refs, which are a little bit less code but you have this edge case of manipulating the DOM, or a state, which definitely cleaner but is a bit more code.






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