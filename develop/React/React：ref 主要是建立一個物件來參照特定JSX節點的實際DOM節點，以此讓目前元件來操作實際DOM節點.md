## 描述
[[@reactRefsHeDOM]]
> Ref 提供了一種可以取得 DOM 節點或在 render 方法內建立 React element 的方式。


> 在典型的 React 資料流裡，props 是 parent component 和 child component 唯一的互動方式。你會藉由使用新的 prop 重新 render 來改變你的 child。然而，有些情況下你需要在典型的資料流以外更改你的 child。這個被更改的 child 可能是 React component 的其中一個 instance，或他可能是個 DOM element。在這兩種情況下，React 提供了「逃生口」


[[@linReactHookBiJi2022]]
> `useRef` returns a mutable ref object whose `.current` property is initialized to the passed argument (`initialValue`). The returned object will persist for the full lifetime of the component.

>useRef 回傳的是一個可變的object，該物件會擁有current這屬性，這屬性的初始值會依照下面的initialVlaue為主，其物件會跟著綁定元件，直到該元件的生命週期結束才被釋放其hook。


```
const something = useRef(initialValue)
```

> with refs, we can set up a connection between a HTML element which is being rendered in the end and our other JS code



重點：
- useRef 是一種hook，綁定於特定元件下，其存活時間會和特定元件一起共存，直到生命週期結束才被釋放其hook
- useRef 主要是在對應元件下，建立一個特定物件去取得JSX元素的對應實際DOM節點，以此讓目前元件來操作實際DOM節點
- useRef 函式本身會回傳一個mutable 物件，裡面夾雜了current屬性，其current屬性值為對應參照的實際DOM節點

### 使用方法


1. 首先要先從react函式庫載入useRefs函式
```
import { useRefs } from 'react';
```

2. 接著在對應的function component，使用useRefs來註冊hook至目前的元件：
	- useRef會產生一個夾雜current屬性的物件，其current屬性值初始值為initialValue
	- 若沒設定initialValue，會是以undefined作為預設值
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


#### 使用案例

假設在一個特定元件下建立useRef這hook，並且拿它回傳的物件去設定專門輸入名字欄位的ref屬性(attribute)，接著做讀取和寫入

讀取輸入名字欄位的節點所擁有的value值：
```
  // 回傳兩個物件，其current屬性值皆因為useRef沒給任何初始值而變成為undefined
  const nameInputRef = useRef()
  const ageInputRef = useRef()

  const submitHandler = (event) => {
      event.preventDefault()
      // current -> the real dom of input for name
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

更新值:
```
nameInputRef.current.value = ''
```

### 使用refs 技術的狀態管理
> uncontrolled components

  
> because they're internal state, so to value which is reflected in them is not controlled by react.
> 	- We rely on the default behavior of the input where a user of course is able to enter something and that entered value is reflected

> nameInputRef.current -> DOM

基於refs來實現狀態管理實際上是基於瀏覽器對於原生DOM元件所會做的狀態管理實現來進行的。所以使用：
	- refs來進行讀取 - 擷取特定DOM節點上的屬性
	- refs來進行寫入 - 直接從DOM節點上的屬性進行寫入和觸發它對應的渲染行為

### useRef 的Ref 縮寫

Refs 是指References

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



#🧠 mutable object 命名緣由 ->->-> `若一個物件被建立之後，物件內容還能夠被修改，該物件就是mutable object`
<!--SR:!2023-10-21,242,248-->

#🧠 immutable object 命名緣由 ->->-> `若一個物件被建立之後，物件內容不能夠被修改，該物件就是immutable object`
<!--SR:!2023-10-27,246,248-->

#🧠 mutable 和 immutable 意思分別為何？ ->->-> `mutable 指的是可改變的 和 immutable 指的是不能被改變的或者不變的 `
<!--SR:!2023-09-01,217,248-->

#🧠 React： useRef 是什麼？->->-> `useRef 是一種hook，綁定於特定元件下，建立一個特定物件去取得JSX元素的對應實際DOM節點，以此讓目前元件來操作實際DOM節點`
<!--SR:!2023-09-27,230,248-->

#🧠  React： useRef 會回傳什麼形式的內容，請盡量詳細說明？ ->->-> `mutable 物件，裡面夾雜了current屬性，其current屬性值為對應參照的實際DOM節點`
<!--SR:!2024-02-04,227,228-->



#🧠 React： const ref1 = useRef(initialValue) 中的initialValue都沒設定的話，會怎麼樣？ ->->-> `會設定undefined作為其初始值。`
<!--SR:!2023-12-27,114,228-->

#🧠 React： const ref1 = useRef(initialValue) 是指什麼？ ->->-> `會在目前元件註冊hook，而useRef會產生一個夾雜current屬性的物件，其current屬性值初始值為initialValue`
<!--SR:!2024-05-23,374,250-->

#🧠 React： 如何利用useRef來讀取名字的輸入欄位  ->->-> `1. 首先要先從react函式庫載入useRefs函式 2. 接著在對應的function component，使用useRefs來註冊hook至目前的元件 3. 在要參照的JSX元素綁定ref屬性，以此獲取JSX的對應實際DOM節點 4. 若要讀取該JSX元素的對應DOM節點的話，可以使用ref1.current，ref1為useRef所回傳的變數`
<!--SR:!2023-09-06,219,248-->

#🧠 React： 如何利用useRef來寫入名字的輸入欄位所顯示的內容  ->->-> `1. 首先要先從react函式庫載入useRefs函式 2. 接著在對應的function component，使用useRefs來註冊hook至目前的元件 3. 在要參照的JSX元素綁定ref屬性，以此獲取JSX的對應實際DOM節點 4. 若要修改該JSX元素的對應DOM節點所擁有的屬性的話，可以使用 // 對著實際DOM節點的屬性增加內容 ref1.current.xxxx = xxxx1`
<!--SR:!2024-11-01,471,250-->




#🧠 React ：基於refs來實現狀態管理是基於什麼基礎來實現？ ->->-> `基於瀏覽器對於原生DOM元件所會做的狀態管理實現來進行的`
<!--SR:!2024-12-08,496,248-->


#🧠 React：使用refs來進行讀取元件資料，實際會是什麼行為？->->-> `擷取特定DOM節點上的屬性`
<!--SR:!2023-12-25,284,248-->

#🧠 React：使用refs來進行對著元件寫入資料，實際會是什麼行為？ ->->-> `直接從DOM節點上的屬性進行寫入和觸發它對應的渲染行為`
<!--SR:!2024-02-28,231,210-->

#🧠 React：useRef 的Ref縮寫是源自什麼？->->-> `Reference`
<!--SR:!2024-12-09,497,248-->


---
Status: #🌱 
Tags:
[[React]] 
Links:
References:
[[@reactRefsHeDOM]]
[[@mdnMutableMDNWeb]]
[[@linReactHookBiJi2022]]