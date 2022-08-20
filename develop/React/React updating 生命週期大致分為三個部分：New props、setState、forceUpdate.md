## 描述


### 生命週期

[[@reactReactComponentReact]]
```
static getDerivedStateFromProps()
shouldComponentUpdate()
render()
getSnapshotBeforeUpdate()
componentDidUpdate()
```


[[@ithomeReactJsRuMen19]]
```
> 1.  static getDerivedStateFromProps(props, state)
> 2.  shouldComponentUpdate(nextProps, nextState)
> 3.  render()
> 4.  getSnapshotBeforeUpdate()
> 5.  渲染畫面
> 6.  componentDidUpdate(prevProps, prevState)
```


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660833335/blog/react/life-cycle/life-cycle-react_wzmir9.jpg)

重點：
- 每一個元件A在對應DOM節點載入(mount)至實際DOM樹之後(換言之，歷經Mounting階段後)，會有三個途徑來變更元件A在實際DOM樹上的DOM節點：
	- New props：由新的props來觸發渲染，由props所夾雜的新資訊來渲染。
	- setState()：根據state是否改變來觸發渲染，由新state的來渲染。
	- forceUpdate()：直接強制渲染，由props和state以外的資料來渲染。
- New props：Updating 完整流程 ：
	- getDerviedStateFromPorps
	- shouldComponentUpdate
	- 更新狀態
	- render
	- getSnapshotBeforeUpdate
	- React updates DOM and refs： 實際DOM節點渲染畫面
	- componentDidUpdate
- setState()：Updating 完整流程：
	- shouldComponentUpdate
	- 更新狀態
	- render
	- getSnapshotBeforeUpdate
	- React updates DOM and refs： 實際DOM節點渲染畫面
	- componentDidUpdate
- forceUpdate()：Updating 完整流程：
	- render
	- getSnapshotBeforeUpdate
	- React updates DOM and refs： 實際DOM節點渲染畫面
	- componentDidUpdate
- updating 子階段：
	- render 階段：getDerivedStateFromProps、shouldComponentUpdate、更新狀態、render
	- pre-commit 階段：getSnapshotBeforeUpdate
	- commit 階段：React updates DOM and refs、componentDidUpdate

- 除了更新狀態、render、 React updates DOM and refs、，其餘開發者可自行開發每個元件下的生命週期函數，若沒設定就保持他們的預設行為

### getDerivedStateFromProps
[[@w3schoolReactLifecycle]]
> The getDerivedStateFromProps() method is called right before rendering the element(s) in the DOM.

```jsx
class Header extends React.Component {
  constructor(props) {
    super(props);
    this.state = {favoritecolor: "red"};
  }
  static getDerivedStateFromProps(props, state) {
    return {favoritecolor: props.favcol };
  }
  render() {
    return (
      <h1>My Favorite Color is {this.state.favoritecolor}</h1>
    );
  }
}

ReactDOM.render(<Header favcol="yellow"/>, document.getElementById('root'));
```

重點：
- 元件A 的 getDerivedStateFromProps 主要會做：
	- 會從該元件A的props接收到源自parent節點所給予的狀態值
	- 將狀態值更新至元件A的this.state
- 預設上是沒有任何處理內容

### shouldComponentUpdate

[[@ithomeReactJsRuMen19]]
> ## shouldComponentUpdate(nextProps, nextState)

> 這個函數的功用像是守門員，用來做確認是不是真的要update。這個函數要return一個布林值。當函數**回傳`false`時，元件就不會更新，也不會繼續執行接下來的`render()`以及剩下的update生命週期函數**。預設會回傳`true`。
> 
> 在這邊，`this.props`和`this.state`是更新之前的，新的props和state在參數中以`nextProps`和`nextState`存在。你可以在這裡對這四者做比較。

[[@reactReactComponentReact]]
> `shouldComponentUpdate()` 會在新的 prop 或 state 被接收之後並在該 component 被 render 之前被呼叫。其預設值是 `true`。這個方法並不會 component 初次 render 時或使用 `forceUpdate()` 時被呼叫。

> `shouldComponentUpdate()` 會在新的 prop 或 state 被接收之後並在該 component 被 render 之前被呼叫


重點：
- 做render之前的確認，如果shouldComponentUpdate回傳true就表示確定要做渲染；反之，若是false就表示確定不做render、react updates dom、componentDidUpdate
- 預設都會回傳true



### 更新狀態

[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]
> 通过我的测试，我发现this.state的值在没有经过更新的情况下，也是可以累加的，再根据您的文章，我觉得我很困惑，这是我的测试连接

[zhuanlan.zhihu.com/p/26](https://zhuanlan.zhihu.com/p/26659511)

> 问题在于：为什么没有经过更新的组件，他的state竟然会在上次的基础上累加呢？您有空能帮我看看我哪里理解错了呢？谢谢


> 谢谢反馈，我之前写得不大严谨，当shouldComponentUpdate函数返回false的时候，更新过程被中段了，render函数就不会被执行了，但是this.state的更新并不会被放弃，并不是在render函数执行中更新this.state，而是在render函数执行之前改变this.state，现在既然shouldComponentUpdate返回false让render失去了执行的机会，React就在这时候把this.state更改了。我在文中更正了文字。


重點：
- 更新狀態階段是在shouldComponentUpdate和render之間的階段
- 無論shouldComponentUpdate回傳什麼，都會更新狀態
- 更新完狀態，才會進入下一階段

### render 
[[@SetStateWeiShiMoBuHuiTongBuGengXinYuanJianZhuangTaiBoXueDao]]
> 每一次setState呼叫都走一圈生命週期，光是想一想也會覺得會帶來效能的問題，其實這四個函式都是純函式，效能應該還好，但是render函式返回的結果會拿去做Virtual DOM比較和更新DOM樹，這個就比較費時間。

> 目前React會將setState的效果放在佇列中，積攢著一次引發更新過程，為的就是把Virtual DOM和DOM樹操作降到最小，用於提高效能。

[[@reactReactComponentReact]]
> 當 render 被呼叫時，它將會檢視 `this.props` 和 `this.state` 中的變化，並回傳以下類別之一：
> -   **React element。** 通常是透過 [JSX](https://zh-hant.reactjs.org/docs/introducing-jsx.html) 建立的。例如，`<div />`和`<MyComponent />`這兩個 React element 會告訴 React 要 render 一個 DOM node 和一個使用者定義的 component。
> -   **Array 和 fragment。** 它們會從 render 中回傳數個 element。細節請參考 [fragment](https://zh-hant.reactjs.org/docs/fragments.html)。
> -   **Portal**。它們讓你將 children render 到不同的 DOM subtree 中。細節請參考 [portal](https://zh-hant.reactjs.org/docs/portals.html)。
> -   **String 和 number。** 這些在 DOM 中將會被 render 為文字 node。
> -   **Boolean 或 `null`。** 什麼都不 render。（此類型主要是支援 `回傳 test && <Child />` 的模式，這裡的 `test` 是一個 boolean 值）。
>  
> `render()` function 應該是 pure 的，這表示：它並不會改變 component 的 state，它在每次呼叫時都會回傳同樣的結果，它並不會直接和瀏覽器有所互動。


重點：
- render 會負責解析目前資訊以及對應元件並得到對應的Virtual DOM

### getSnapshotBeforeUpdate

[[@w3schoolReactLifecycle]]
> In the `getSnapshotBeforeUpdate()` method you have access to the `props` and `state` _before_ the update, meaning that even after the update, you can check what the values were _before_ the update.


[[@reactReactComponentReact]]
> `getSnapshotBeforeUpdate()` 在提交最新 render 的 output 之前立即被調用。它讓你在 DOM 改變之前先從其中抓取一些資訊

重點：
- 元件A 的 getSnapshotBeforeUpdate 主要用途：
	- 專門獲取元件A畫面更新前的資訊、狀態、props 來做處理
- 預設上是沒有任何處理內容
- 在提交render的輸出之前會被調用



### React updates DOM and refs： 實際DOM節點渲染畫面
重點：
- 實際DOM節點渲染畫面的主要用途：
	- 比較差異：拿render獲取到的Virtual DOM與目前的Virtual DOM做比較差異
	- 針對差異來更新實際DOM：直接拿差異結果來以實際DOM節點轉換成對應渲染指令，接著執行



### componentDidUpdate

[[@reactReactComponentReact]]
> `componentDidUpdate()` 會在更新後馬上被呼叫。這個方法並不會在初次 render 時被呼叫。

[[@w3schoolReactLifecycle]]
> The `componentDidUpdate` method is called after the component is updated in the DOM.

重點：
- 元件A 的 componentDidUpdate 主要用途為：
	- 主要指定在更新對應元件的畫面後要做些什麼
- 預設上是沒有任何處理內容


## 複習
#🧠 歷經Mounting階段後，會有三個途徑來變更元件A在實際DOM樹上的DOM節點，請問目前是處於什麼life cycle？ ->->-> `updating`
<!--SR:!2022-08-23,3,250-->

#🧠 歷經Mounting階段後，會有三個途徑來變更元件A在實際DOM樹上的DOM節點，請問會有哪三個途徑？ ->->-> `New props：由新的props來觸發渲染、setState()：根據state是否改變來觸發渲染 forceUpdate()：直接強制渲染，由props和state以外的資料來渲染。`
<!--SR:!2022-08-23,3,250-->

#🧠  歷經Mounting階段後，會有三個途徑來變更元件A在實際DOM樹上的DOM節點，請問三途徑之一的New props 拿什麼資料來渲染畫面？->->-> `props夾雜的新資訊`
<!--SR:!2022-08-23,3,250-->

#🧠 歷經Mounting階段後，會有三個途徑來變更元件A在實際DOM樹上的DOM節點，請問三途徑之一的setState 拿什麼資料來渲染畫面？ ->->-> `狀態`
<!--SR:!2022-08-23,3,250-->

#🧠 歷經Mounting階段後，會有三個途徑來變更元件A在實際DOM樹上的DOM節點，請問三途徑之一的 **forceUpdate()** 拿什麼資料來渲染畫面？ ->->-> `由props和state以外的資料來渲染`
<!--SR:!2022-08-23,3,250-->


#🧠 react updating 階段若使用new props的流程會是什麼？ ->->-> ` - getDerviedStateFromPorps、- shouldComponentUpdate - 更新狀態 - render - getSnapshotBeforeUpdate - 實際DOM節點渲染畫面 - componentDidUpdate`
<!--SR:!2022-08-23,3,250-->

#🧠 react updating 子階段中的render包含哪些步驟？ ->->-> `getDerivedStateFromProps、shouldComponentUpdate、更新狀態、render`
<!--SR:!2022-08-23,3,250-->


#🧠 react updating 子階段中的pre-commit包含哪些步驟？ ->->-> `getSnapshotBeforeUpdate`
<!--SR:!2022-08-23,3,250-->

#🧠 react updating 子階段中的commit包含哪些步驟？->->-> `React updates DOM and refs、componentDidUpdate`
<!--SR:!2022-08-23,3,250-->


#🧠  react updating 階段若使用setState的流程會是什麼？ ->->-> `-shouldComponentUpdate - 更新狀態 - render - getSnapshotBeforeUpdate - 實際DOM節點渲染畫面 - componentDidUpdate`
<!--SR:!2022-08-23,3,250-->

#🧠 react updating 階段若使用forceUpdate()的流程會是什麼？ ->->-> `- render - getSnapshotBeforeUpdate - 實際DOM節點渲染畫面 - componentDidUpdate`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的getDerivedStateFromProps是做什麼用的？->->-> `	- 會從該元件A的props接收到源自parent節點所給予的狀態值 - 將狀態值更新至元件A的this.state`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的getDerivedStateFromProps採用預設的話，會是什麼？ ->->-> ` 預設上是沒有任何處理內容`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 shouldComponentUpdate是做什麼用的？ ->->-> `做render之前的確認，如果shouldComponentUpdate回傳true就表示確定要做渲染；反之，若是false就表示確定不做渲染`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 shouldComponentUpdate回傳true就表示？ ->->-> `做渲染`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 shouldComponentUpdate回傳false就表示？  ->->-> `不執行render、react updates dom、componentDidUpdate`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 shouldComponentUpdate回傳false就還做不做狀態更新 ->->-> `做`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的shouldComponentUpdate採用預設的話，會是什麼？ ->->-> `會直接回傳true`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的**更新狀態** 何時會做？ ->->-> `通常會於shouldComponentUpdate和render之間。`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的**更新狀態** 是會做什麼？ ->->-> `無論shouldComponentUpdate回傳什麼，都會更新狀態，更新完狀態，才會進入下一階段`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的**render** 是會做什麼？(資訊和畫面)->->-> `會負責解析目前資訊以及對應元件並得到對應的Virtual DOM`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的**getSnapshotBeforeUpdate** 是會做什麼？ ->->-> `專門獲取元件A畫面更新前的資訊、狀態、props 來做處理`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 getSnapshotBeforeUpdate採用預設的話，會是什麼？ ->->-> `預設上是沒有任何處理內容`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的 React updates DOM and refs 是會做什麼？ ->->-> `比較差異：拿render獲取到的Virtual DOM與目前的Virtual DOM做比較差異、針對差異來更新實際DOM：直接拿差異結果來以實際DOM節點轉換成對應渲染指令，接著執行`
<!--SR:!2022-08-23,3,250-->

#🧠 react 生命週期中會用到的componentDidUpdate 是會做什麼？ ->->-> `主要指定在更新對應元件的畫面後要做些什麼`
<!--SR:!2022-08-21,1,230-->

#🧠 react 生命週期中會用到的 componentDidUpdate採用預設的話，會是什麼？ ->->-> `預設上是沒有任何處理內容`
<!--SR:!2022-08-23,3,250-->

---
Status: #🌱  
Tags:
[[React]] - [[JavaScript]]
Links:
[[life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：mounting 階段、updating階段、umounting階段]]
References:
[[@w3schoolReactLifecycle]]
[[@ithomeReactJsRuMen19]]
[[@reactReactComponentReact]]
[[@SetStateWeiShiMoBuHuiTongBuGengXinYuanJianZhuangTaiBoXueDao]]
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]