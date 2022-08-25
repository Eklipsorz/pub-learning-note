## 描述

### dumb componet & presentational component

[[@tabrishelexQianDuanDumbComponents]]
> Dumb components 也被叫做 'presentational' components，因为它们仅仅被用来呈现一些 DOM。一旦展示工作完成，component 就不再发生变化。

> 这些 component 只有一个 render() 方法（他们不需要其他东西），有时仅仅是一个 Javascript 函数。他们没有内部 state 需要管理。当有用户操作时，它们不知道如何响应和更新数据。无知万岁！


重點：
- dumb 意味著傻子、啞巴
- 原本component本身具有渲染、業務邏輯(含事件處理)，而dumb形容component是指該component 只會負責特定事物的渲染和渲染相關的業務邏輯，即使有人對component做出互動，他們本身也沒辦法透過互動來重新以互動結果來渲染自己
- 在React 上， dumb component 是：
	- 沒註冊任何狀態、更新狀態用的函式
	- 不會對任何元件進行狀態管理/更新
	- 只會從props給予資訊或者預設內容來渲染固定畫面，一渲染完畢之後，就不會再發生變化
- 由於dumb component本身只會渲染，所以又稱之為prsentational component。


###  Smart Components
[[@tabrishelexQianDuanDumbComponents]]

> 另一方面，Smart components（或称为 container components）承担了其他任务。为了对得起自己 smart 的牌面，它们需要跟踪状态并且关心 app 的工作情况。

> 由于使用容器设计模式，container 组件可以被分成若干个处理自己呈现内容的 presentational component。container component 处理繁重的逻辑，将数据通过 props 传到下属的 presentational component。

> 它们是基于类的（class-based）组件，它们在 constructor() 中定义了自己的 state。

```js
class App extends Component {
  constructor(props){
    super(props);
    this.state = {pictures : []};
  }
}
```

> 这些组件经常也会包含一些其他的回调函数，它们被用来更新 state 以及传递更新到子组件上。

> 根组件就是 smart component 的一个好例子。它通常负责为整个 app 维护若干个 state，并需要将一些额外的 function 传递到子组件中，使用户与网站交互时可以更新这些 state。


- stateless component 別名為 dumb component / presentational component
	- 稱之為prsentational component，是因為component只用做於呈現用途上的元件，一旦呈現完畢之後，就不會有任何變化



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@tabrishelexQianDuanDumbComponents]]