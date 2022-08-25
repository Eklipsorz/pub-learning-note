## 描述
[[@ithomeDay06WangYeDeXiaoLingJianComponents]]
> React 有兩種組件，分別是帶狀態的（stateful components）和沒有狀態的（stateless components）組件，前者效能較差，原因是他除了狀態本身以外，另外還帶有狀態相關的行為函式，後者因為沒有這些，只是單純的接收狀態並繪製出來，效能上自然就比較好一些


[[@codecademyReactComponentState]]
> In React, a _stateful_ component is a component that holds some state. _Stateless_ components, by contrast, have no state. Note that both types of components can use props.

> In the example, there are two React components. The `Store` component is stateful and the `Week` component is stateless.


```
class Store extends React.Component {

  constructor(props) {
    super(props);
    this.state = { sell: 'anything' };
  }

  render() {
    return <h1>I'm selling {this.state.sell}.</h1>;
  }

}

class Week extends React.Component {

  render() {
    return <h1>Today is {this.props.day}!</h1>;
  }

}
```


重點：
- stateful component 是指元件本身註冊狀態、更新狀態用的函式
- stateless component  是指元件本身沒有註冊狀態、更新狀態用的函式，但可以透過props去接收其他元件下的狀態
	- stateless component 被稱之為dumb component、presentational component

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：dumb component 本身負責接收資訊來渲染內容的元件，並不負責改變其他元件的渲染內容，smart component是相對於dumb component，會負責控管child component的狀態並根據互動結果來改變child component]]
References:
[[@ithomeDay06WangYeDeXiaoLingJianComponents]]
[[@codecademyReactComponentState]]