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


### render
> 每一次setState呼叫都走一圈生命週期，光是想一想也會覺得會帶來效能的問題，其實這四個函式都是純函式，效能應該還好，但是render函式返回的結果會拿去做Virtual DOM比較和更新DOM樹，這個就比較費時間。

> 目前React會將setState的效果放在佇列中，積攢著一次引發更新過程，為的就是把Virtual DOM和DOM樹操作降到最小，用於提高效能。

### shouldComponentUpdate

[[@ithomeReactJsRuMen19]]
> ## shouldComponentUpdate(nextProps, nextState)

> 這個函數的功用像是守門員，用來做確認是不是真的要update。這個函數要return一個布林值。當函數**回傳`false`時，元件就不會更新，也不會繼續執行接下來的`render()`以及剩下的update生命週期函數**。預設會回傳`true`。
> 
> 在這邊，`this.props`和`this.state`是更新之前的，新的props和state在參數中以`nextProps`和`nextState`存在。你可以在這裡對這四者做比較。

[[@reactReactComponentReact]]
> `shouldComponentUpdate()` 會在新的 prop 或 state 被接收之後並在該 component 被 render 之前被呼叫。其預設值是 `true`。這個方法並不會 component 初次 render 時或使用 `forceUpdate()` 時被呼叫。

> `shouldComponentUpdate()` 會在新的 prop 或 state 被接收之後並在該 component 被 render 之前被呼叫




---
Status: #🌱  
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@ithomeReactJsRuMen19]]
[[@reactReactComponentReact]]
[[@SetStateWeiShiMoBuHuiTongBuGengXinYuanJianZhuangTaiBoXueDao]]