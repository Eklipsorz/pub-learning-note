## 描述










## 生命週期
當 prop 或 state 有變化時，就會產生更新。當一個 component 被重新 render 時，其生命週期將會依照下列的順序呼叫這些方法：
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

>

重點：

- 流程：
	- getDerviedStateFromPorps
	- shouldComponentUpdate
	- 更新狀態
	- render
	- getSnapshotBeforeUpdate
	- 實際DOM節點渲染畫面
	- componentDidUpdate

### componentDidUpdate


### 更新狀態

[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]
> 通过我的测试，我发现this.state的值在没有经过更新的情况下，也是可以累加的，再根据您的文章，我觉得我很困惑，这是我的测试连接

[zhuanlan.zhihu.com/p/26](https://zhuanlan.zhihu.com/p/26659511)

> 问题在于：为什么没有经过更新的组件，他的state竟然会在上次的基础上累加呢？您有空能帮我看看我哪里理解错了呢？谢谢


> 谢谢反馈，我之前写得不大严谨，当shouldComponentUpdate函数返回false的时候，更新过程被中段了，render函数就不会被执行了，但是this.state的更新并不会被放弃，并不是在render函数执行中更新this.state，而是在render函数执行之前改变this.state，现在既然shouldComponentUpdate返回false让render失去了执行的机会，React就在这时候把this.state更改了。我在文中更正了文字。


重點：
- 更新狀態階段是在shouldComponentUpdate和render之間的階段
- 無論shouldComponentUpdate回傳什麼，都會更新狀態
- 更新完狀態，才會進入render階段

### render & 渲染畫面
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
- render 會負責解析對應元件並得到對應的Virtual DOM
- 渲染畫面：
	- 比較差異：拿render獲取到的Virtual DOM與目前的Virtual DOM做比較差異
	- 針對差異來更新實際DOM：直接拿差異結果來以實際DOM節點轉換成對應渲染指令，接著執行
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
- 做render之前的確認，如果shouldComponentUpdate回傳true就表示確定要做渲染；反之，若是false就表示確定不做炫染

---
Status: #🌱  
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@ithomeReactJsRuMen19]]
[[@reactReactComponentReact]]
[[@SetStateWeiShiMoBuHuiTongBuGengXinYuanJianZhuangTaiBoXueDao]]
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]