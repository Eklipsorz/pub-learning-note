## 描述
[[@chenlongWeiShiMereactHereactdomYaoFenChengLiangGeBaoZhiHu]]
> React在v0.14之前是没有react-dom的，所有功能都包含在react里。从v0.14(2015-10)开始，react才被拆分成react和react-dom。为什么要把react和react-dom分开呢？因为有了react-native。react只包含了Web和Mobile通用的核心部分，负责Dom操作的分到react-dom中，负责Mobile的包含在react-native中。


> 因为React并不只用于浏览器，当后来发展被应用到其他平台上时候，渲染层就不一定是浏览器dom操作了，比如React native。于是dom操作层，也可理解成具体实施渲染的层就被隔离出来了，单独打包，按需引用。


> 对于具有跨平台能力的 React 体系来说，分包可以将抽象逻辑与平台实现分开。

> react 包即是抽象逻辑，它包含了 React 的主干逻辑。例如组件实现、更新调度等。

> react-dom 顾名思义就是一种针对 dom 的平台实现，主要用于在 web 端进行渲染。

> 而声名在外的 react-native 则是原生应用实现，可以通过 react-native 内部的相应机制与操作系统进行通信来调用原生控件进行渲染。

> 这是一个**依赖倒置**原则的典型应用，**高层模块不应依赖底层模块的具体实现**。简单来说，就是我们只需要将组件按一定的形式编写好，而最终 render 函数是以怎样的机制将 JSX 渲染到页面上的，我们不需要关心，只要这个机制同样遵循我编写组件所依赖的规则就好——这个规则就是 react。


重點：
- React 本身可以在其他用來操作畫面的介面上進行操作，其介面比如說網頁的DOM、React native所建立的畫面存取介面
- 由於react本身支援較多的渲染介面，然而開發者本身並不會用到太多介面，所以React 為了根據開發者根據所需的介面來選擇，所以會額外區分成react-dom來表示支援網頁的DOM，而被抽離出來的react本身是支援核心部分的功能
- 總結：
	- react-dom本身是支援網頁dom和瀏覽器操作的函式庫
	- react 本身是核心部分的功能
	- 切分原因則是因為react本身支援介面就很多，為了很好專注在不同介面的渲染，所以額外切分


## 複習
#🧠 React ：請問React支援哪些渲染畫面的介面？ ->->-> `網頁的DOM模型、由React Native所建立的畫面存取介面`
<!--SR:!2022-08-22,10,250-->

#🧠 React：請問React 為什麼要切分成react和react-dom這兩個函式庫？->->-> `由於react本身支援較多的渲染介面，然而開發者本身並不會用到太多介面，所以React 為了根據開發者根據所需的介面來選擇，所以會額外區分成react-dom來表示支援網頁的DOM，而被抽離出來的react本身是支援核心部分的功能`
<!--SR:!2022-08-13,3,250-->


#🧠 React：react 和 react-dom 的用途大致上是什麼？ ->->-> `	- react-dom本身是支援網頁dom和瀏覽器操作的函式庫 - react 本身是核心部分的功能`
<!--SR:!2022-08-22,10,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@chenlongWeiShiMereactHereactdomYaoFenChengLiangGeBaoZhiHu]]