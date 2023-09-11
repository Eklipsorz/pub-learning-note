## 描述


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660833335/blog/react/life-cycle/life-cycle-react_wzmir9.jpg)

### 生命週期

Mounting 階段是每一個元件轉換成對應DOM結構差入至目前DOM Tree進行渲染的階段，class-based component 相對應的流程(函式)會有：
- constructor
- getDerivedStateFromProps
- render
- React updates DOM & refs
- componentDidMount

除了React updates DOM & refs以外，其餘預設是沒有內容，必須手動設置

### constructor
[[@reactReactComponentReact]]
> 通常在 React 中 constructor 只會有兩種用途：
> -  透過指定一個 this.state 物件來初始化內部 state。
> - 為 event handler 方法綁定 instance。

> 請不要在 constructor() 中呼叫 setState()。如果你的 component 需要使用內部 state，請在 constructor 中將其最初的 state 指定為 this.state：

```
constructor(props) {
  super(props);
  // 不要在這裡呼叫 this.setState()！
  this.state = { counter: 0 };
  this.handleClick = this.handleClick.bind(this);
}
```


重點：
- constructor 主要用途為
	- 建立根據元件的prototype來建立元件實例
	- 初始化元件實例設定各自的狀態、事件綁定處理


#### this.setState 和 this.state 在哪個位置設定

[[@reactReactComponentReact]]
> Constructor 是唯一一個你應該直接指定 this.state 的地方。在所有其他的方法中，你則需要使用 this.setState()。

在class component 開發方式中：
- this.state 和 this.setState 之間的作用：
	- this.state 是儲存目前狀態值的變數，而非真正儲存狀態的特殊變數
	- this.setState會是更新this.state、更新元件儲存狀態的狀態變數、觸發渲染的函式
- 建議開發方式為
	- 在constructor設定this.state
	- 其餘地方使用this.setState來變更狀態、觸發渲染

### getDerivedStateFromProps
[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]

getDerivedStateFromProps 主要用途為：
	- 從該元件的props物件獲取狀態
	- 並用獲取到的狀態值更新目前元件的狀態
- 預設沒有任何處理內容。

### render & React updates DOM and refs 


[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]

render 主要用途為：
- 根據實例內容和render上對應元件的內容來解析成Virtual DOM結果

React updates DOM and refs 主要用途為：
- 拿render獲取到的Virtual DOM結果和目前的Virtual DOM結果比對，看差異是如何
- 根據差異來轉換成實際DOM節點來渲染



### componentDidMount
[[@reactReactComponentReact]]
> 在一個 component 被 mount（加入 DOM tree 中）後，`componentDidMount()` 會馬上被呼叫

重點
- componentDidMount 主用途為
	- 指定對應元件的實際DOM節點加入至DOM tree之後所要做的事情。
- 預設沒有任何處理內容。



## 複習
#🧠 React Mounting 階段算是生命週期的一部分嗎？ ->->-> `對`
<!--SR:!2024-11-02,494,250-->

#🧠 React Mounting 階段是什麼？ ->->-> `是每一個元件轉換成對應DOM結構差入至目前DOM Tree進行渲染的階段`
<!--SR:!2024-11-22,508,250-->

#🧠 React Mounting 階段在class-based component的流程有什麼 ->->-> `constructor、getDerivedStateFromProps、render、React updates DOM & refs、componentDidMount`
<!--SR:!2023-10-09,27,150-->

#🧠 constructor、getDerivedStateFromProps、render、React updates DOM & refs、componentDidMount 是函式嗎？ ->->-> `對`
<!--SR:!2023-11-18,275,250-->

#🧠 React Mounting 階段下的constructor函式是做什麼？ (實例、狀態、綁定)->->-> `- 建立根據元件的prototype來建立元件實例 - 初始化元件實例設定各自的狀態、事件綁定處理`
<!--SR:!2024-07-11,423,250-->


#🧠 在class component 開發方式中，this.state 和 this.setState 是什麼？ ->->-> `前者是儲存目前狀態值的變數、this.setState會是更新this.state、更新元件儲存狀態的狀態變數、觸發渲染的函式`
<!--SR:!2023-09-24,216,229-->

#🧠 在class component 開發方式中，this.state 和 this.setState 被建議放在哪？ ->->-> `this.state 建議載constructor定義，剩餘要更改狀態並重新渲染就透過this.setState`
<!--SR:!2023-10-10,251,249-->


#🧠 React Mounting 階段下的render函式是做什麼？ ->->-> `根據實例內容和render上對應元件的內容來解析成Virtual DOM結果`
<!--SR:!2023-06-18,189,250-->

#🧠 React Mounting 階段下的React updates DOM and refs函式是做什麼？ ->->-> `- 拿render獲取到的Virtual DOM結果和目前的Virtual DOM結果比對，看差異是如何 - 根據差異來轉換成實際DOM節點來渲染`
<!--SR:!2023-11-12,207,230-->

#🧠 React Mounting 階段下的componentDidMount函式是做什麼？ ->->-> `指定對應元件的實際DOM節點加入至DOM tree之後要做的事情`
<!--SR:!2024-05-01,248,230-->

#🧠 React Mounting 階段下的componentDidMount函式預設是做什麼？ ->->-> `預設沒有任何處理內容。`
<!--SR:!2025-02-26,556,250-->

#🧠 React Mounting 階段下的getDerivedStateFormProps函式主要用途是做什麼？ ->->-> `	- 從該元件的props物件獲取狀態 - 並用獲取到的狀態值更新目前元件的狀態`
<!--SR:!2024-03-21,215,230-->

#🧠 React Mounting 階段下的getDerivedStateFormProps函式預設是做什麼？ ->->-> `預設沒有任何處理內容。`
<!--SR:!2023-12-22,109,230-->


#🧠 React Mounting 階段下的子階段render有什麼 ->->-> `constructor、getDerivedStateFromProps、render`
<!--SR:!2023-11-28,85,210-->

#🧠 React Mounting 階段下的子階段pre-commit有什麼 ->->-> `沒`
<!--SR:!2025-03-12,573,250-->

#🧠 React Mounting 階段下的子階段commit有什麼 ->->-> `React Updates DOM & refs、componentDidMount`
<!--SR:!2023-07-11,189,230-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：mounting 階段、updating階段、umounting階段]]
[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]
[[React Unmounting 階段是指特定元件的實際DOM節點從實際DOM Tree被移除的階段]]
References:
[[@reactReactComponentReact]]