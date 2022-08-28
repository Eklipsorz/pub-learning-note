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
- stateful component 概念上是指能夠對狀態進行處理、控管的元件
- stateless component 概念上是指不對狀態進行處理、控管的元件
- stateful component 是指元件本身註冊狀態、更新狀態用的函式
- stateless component  是指元件本身沒有註冊狀態、更新狀態用的函式，也不會控管其他元件的狀態，但可以透過props去接收其他元件下的狀態
	- stateless component 被稱之為dumb component、presentational component



### stateful && stateless 命名緣由

[[@Stateful2021]] stateful
> That supports different states, reacting to the same input differently depending on the current state.

[[@Stateless2022]] stateless
>(computer science) Of a system or protocol, such that it does not keep a persistent state between transactions. 


重點：
- stateful ：在電腦科學裡，是指支持不同狀態並依據狀態的不同來進行處理
- stateless：stateful 的反義詞，主要描述不依據狀態來進行處理


## 複習

#🧠 stateful 在電腦科學裡的意思？ ->->-> `是指支持不同狀態並依據狀態的不同來進行處理或者能夠對狀態進行處理、控管`
<!--SR:!2022-09-01,4,248-->

#🧠 stateless 在電腦科學裡的意思？ ->->-> `stateful 的反義詞，主要描述不依據狀態來進行處理`
<!--SR:!2022-08-29,3,250-->

#🧠 stateful component 概念 是什麼？ ->->-> `是指能夠對狀態進行處理、控管的元件`
<!--SR:!2022-09-01,4,248-->

#🧠 stateless component 概念 是什麼？ ->->-> `是指不對狀態進行處理、控管的元件`
<!--SR:!2022-08-29,3,250-->

#🧠 在React中，stateful component 是什麼？ ->->-> `是指元件本身註冊狀態、更新狀態用的函式`
<!--SR:!2022-09-01,4,248-->

#🧠 在React中，stateless component 是什麼？   ->->-> `是指元件本身沒有註冊狀態、更新狀態用的函式，是指元件本身沒有註冊狀態、更新狀態用的函式，也不會控管其他元件的狀態，但可以透過props去接收其他元件下的狀態`
<!--SR:!2022-08-29,2,230-->

#🧠 在React中，若 stateless component 可以透過props來接收別人更新狀態用的函式，還能叫stateless component嗎？ ->->-> `不能`
<!--SR:!2022-09-02,5,248-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：dumb component 本身負責接收資訊來渲染內容的元件，並不負責改變其他元件的渲染內容，smart component是相對於dumb component，會負責控管child component的狀態並根據互動結果來改變child component]]
References:
[[@ithomeDay06WangYeDeXiaoLingJianComponents]]
[[@codecademyReactComponentState]]
[[@Stateful2021]]
[[@Stateless2022]]