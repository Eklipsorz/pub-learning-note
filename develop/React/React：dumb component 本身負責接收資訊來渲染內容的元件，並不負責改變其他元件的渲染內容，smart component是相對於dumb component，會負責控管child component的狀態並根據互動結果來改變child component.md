## 描述

### dumb componet & presentational component

[[@tabrishelexQianDuanDumbComponents]]
> Dumb components 也被叫做 'presentational' components，因为它们仅仅被用来呈现一些 DOM。一旦展示工作完成，component 就不再发生变化。

> 这些 component 只有一个 render() 方法（他们不需要其他东西），有时仅仅是一个 Javascript 函数。他们没有内部 state 需要管理。当有用户操作时，它们不知道如何响应和更新数据。无知万岁！


重點：
- dumb 意味著傻子、啞巴
- 原本component本身具有渲染、業務邏輯(含事件處理)，而dumb形容component是指該component 只會負責特定事物的渲染和渲染相關的業務邏輯，即使有人對component做出互動，他們本身也沒辦法透過互動來重新以互動結果來渲染自己、其他component
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

重點：
- smart components 是相對於 dumb components 的稱呼
- smart component 本身會有渲染、業務邏輯，只要有人對其component做出互動，他們本身可以透過互動來重新以互動結果來渲染自己、其他child component，也就是由該component來控管每個child component的渲染內容
- 在React 上， dumb component 是：
	- 註冊狀態、更新狀態用的函式
	- 負責對它所包含的子元件進行狀態管理/更新
	- 皆由狀態更新來負責渲染子元件
- 也可稱之為container component

## 複習
#🧠 dumb component 是什麼？ ->->-> `dumb形容component是指該component 只會負責特定事物的渲染和渲染相關的業務邏輯，即使有人對component做出互動，他們本身也沒辦法透過互動來重新以互動結果來渲染自己、其他component`
<!--SR:!2023-08-05,210,248-->

#🧠 在React 上， dumb component 是什麼元件？ ->->-> `沒註冊任何狀態、更新狀態用的函式、不會對任何元件進行狀態管理/更新、 只會從props給予資訊或者預設內容來渲染固定畫面，一渲染完畢之後，就不會再發生變化`
<!--SR:!2023-08-27,221,248-->

#🧠 在React 上， dumb component 的別名是什麼？為什麼->->-> `由於dumb component本身只會渲染，所以又稱之為prsentational component。`
<!--SR:!2023-11-02,225,228-->

#🧠 smart component是什麼？ ->->-> `smart components 是相對於 dumb components 的稱呼，smart component 本身會有渲染、業務邏輯，只要有人對其component做出互動，他們本身可以透過互動來重新以互動結果來渲染自己、其他child component，也就是由該component來控管每個child component的渲染內容`
<!--SR:!2023-11-04,264,248-->

#🧠 在React 上， smart component 是什麼元件？ ->->-> `註冊狀態、更新狀態用的函式、負責對它所包含的子元件進行狀態管理/更新、皆由狀態更新來負責渲染子元件`
<!--SR:!2023-11-23,88,210-->

#🧠 在React 上， smart component  的別名是什麼？->->-> `container component`
<!--SR:!2023-07-20,66,208-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：stateful component 是指本身註冊狀態以及對應狀態更新用函式，stateless component則是指本身沒有註冊狀態和沒註冊更新狀態用的函式]]
References:
[[@tabrishelexQianDuanDumbComponents]]