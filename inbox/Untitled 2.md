## 描述

### provider vs. consumer vs. context 角色
[[@ithomeWantKnowReacta]]
> ### Context 角色

> React context 的使用會環繞三個角色在運作：
>
> -   Context Object
> -   Provider
> -   Consumer

> 一個 React app 中可以有多個 React context。每個 React context 的本體都是一個物件（在這邊把它稱為 context object）。其中 context object 中又會有兩個很重要的屬性：Provider（提供者）與 Consumer（消費者）。
>
> -   Provider（提供者）的功用就是用來**提供** context 值。
> -   Consumer（消費者）的功用則是用來**使用** context 值。

重點：
- Context Object：目前是定義狀態的環境，內容主要會由Provider或者預設狀態來提供
- Provider：提供特定狀態值至Context Object
- Consumer：向Context Object訂閱/監聽並存取Context Object上的狀態值


### Provider component
[[@reactContextReact]]

> ### `Context.Provider`

```
<MyContext.Provider value={/* some value */}>
```

> Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.

> The Provider component accepts a `value` prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.

重點：
1. 每個 context object 都會有 provider component ：
	- 是一個wrapper component
	- 由於Context Object的具體內容會由Provider component所提供的狀態值，所以它本身可以代表著Context object的component
	- 被它包覆著的子節點都允許存取其Context Object(PS. 只是允許，而非真的存取)或者Context Object對於這些子節點是可見的
	- 沒被它包覆著子節點不被允許存取其Context Object


### Consumer component
> Context.Consumer

```
<MyContext.Consumer>
  {value => /* render something based on the context value */}
</MyContext.Consumer>
```
> A React component that subscribes to context changes. Using this component lets you subscribe to a context within a function component.

重點：
1. 每個 context object 都會有consumer component：
	- 是一個wrapper component
	- 訂閱/監聽對應context
	- 提供特定方法讓被包含的子節點能夠存取對應的context所擁有的值：
		- 以callback + 第一個引數為context object本身，其屬性值會是代表著狀態、更新用狀態函式
	```
	<Context.Consumer>
		{(context) => .....}
	</Context.Consumer>
	```


### Context object


> Context is itself is not a component
  
[[@reactContextReact]]
const MyContext = React.createContext(defaultValue);

> Creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching `Provider` above it in the tree.

> The `defaultValue` argument is **only** used when a component does not have a matching Provider above it in the tree. This default value can be helpful for testing components in isolation without wrapping them.
  

重點：
- createContext 建立一個context 物件，會回傳對應context 物件。
- defaultValue 是定義初始狀態為何，形式可以是數字、字串、物件，通常為物件
- 當React 開始渲染一個元件時，而該元件訂閱該context object，則
- ~~當React 開始渲染一個元件時，而該元件訂閱該context物件，則會讓其讀取離它(Virtual DOM)較近的Provider元件來獲取目前context 內容。~~




## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: