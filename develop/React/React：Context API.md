## 描述
React Context
1. 元件間的內建狀態儲存器
2. 在不依賴額外的props chain的情況下，實現元件間彼此交換狀態和觸發渲染
3. 在不依賴額外的props chain的情況下，元件之間的狀態、更新狀態用函式可以直接透過Context面對面交換。


1. component-wide "behind the scenes", state storage, built into React

2. and this then allows us to, for example, trigger a action in that component-wide State Storage, then directly pass that to the component

3. without build such a long prop chain


舉例：
- Login登入後，就會將狀態發送至state storage，然後再由state storage直接發送至shop元件
- 增加產品至購物車後，就將狀態發送至state storage，然後再由state storage直接發送至cart元件
- 從中不再依賴著props所建立的chain


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663607881/blog/react/context/component-wide-state-storage_caeat2.png)



Provider
[[@reactContextReact]]

> ### `Context.Provider`

```
<MyContext.Provider value={/* some value */}>
```

> Every Context object comes with a Provider React component that allows consuming components to subscribe to context changes.

> The Provider component accepts a `value` prop to be passed to consuming components that are descendants of this Provider. One Provider can be connected to many consumers. Providers can be nested to override values deeper within the tree.


### Context object


> Context is itself is not a component
  
[[@reactContextReact]]
const MyContext = React.createContext(defaultValue);

> Creates a Context object. When React renders a component that subscribes to this Context object it will read the current context value from the closest matching `Provider` above it in the tree.

> The `defaultValue` argument is **only** used when a component does not have a matching Provider above it in the tree. This default value can be helpful for testing components in isolation without wrapping them.
  

重點：
- createContext 建立一個context 物件，會回傳對應context 物件。
- defaultValue 是定義初始狀態為何，形式可以是數字、字串、物件，通常為物件
- ~~當React 開始渲染一個元件時，而該元件訂閱該context物件，則會讓其讀取離它(Virtual DOM)較近的Provider元件來獲取目前context 內容。~~





### context 命名緣由
context：
> **the situation within which something exists or happens, and that can help explain it**


重點：
- context 是指場景，一個透過某個事物A所存在或者所發生的場景來解釋某個事物
- 在電腦科學裡，可衍生成定義某個事物A的環境
### xxxx-wide 命名緣由

> -wide combines with nouns to form adjectives which indicate that something exists or happens throughout the place or area that the noun refers to. 

重點：

- xxx-wide ：-wide會與名詞來形成一個形容詞來表示特定事物存在於/特定事物發生在xxx所指的區域 或者指的是 xxx所指的區域之範圍內

- component-wide：元件範圍內



context => 定義如何執行的資訊

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：使用如Redux或者Context這種集中狀態機制是為了讓多個元件下能夠彼此共享狀態和彼此觸發渲染週期]]
[[React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染]]
References:
[[@reactContextReact]]