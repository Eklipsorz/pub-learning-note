
## 描述


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660833335/blog/react/life-cycle/life-cycle-react_wzmir9.jpg)

[[@hussainAnswerReactLifecyle2021]] 
> Render phase: Is used to calculate changes, and may be aborted if the user wants to. If this phase is aborted the DOM isn’t updated.

> Pre-commit phase: Is a period where you can read changes made to the VDOM, before they are applied to the actual DOM.

> Commit phase: Here the changes are applied and any side effects are triggered.

重點：
- react 生命階段主要是 mounting -> updating -> unmounting
- 每一個階段又可以在分成三個子階段：
	- render phase：一開始的階段，主要是確定元件在Virtual DOM上的對應結構
	- pre-commit phase：在提交render phase所產生的結構進行實際DOM渲染之前的階段
	- commit phase：提交render phase所產生的結構並進行實際DOM渲染的階段，在這裡就是把暫時性對於DOM的修改轉換成永久性的DOM修改

## 複習
#🧠 react 生命階段會有哪些過程 ->->-> ` mounting -> updating -> unmounting`
<!--SR:!2023-06-20,190,250-->

#🧠 react 生命階段會有mounting -> updating -> unmounting，那麼每一個階段又可以切分成三個子階段，是哪三個？->->-> `render phase、pre-commit phase、commit phase`
<!--SR:!2024-02-09,325,250-->

#🧠 react 生命階段中的子階段render phase會是什麼？ ->->-> `一開始的階段，主要是確定元件在Virtual DOM上的對應結構`
<!--SR:!2025-04-24,590,250-->

#🧠 react 生命階段中的子階段pre-commit phase 會是什麼？->->-> `在提交render phase所產生的結構進行實際DOM渲染之前的階段`
<!--SR:!2023-05-14,163,250-->

#🧠 react 生命階段中的子階段commit phase會是什麼？ ->->-> `提交render phase所產生的結構並進行實際DOM渲染的階段`
<!--SR:!2023-07-13,185,230-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]
[[life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：mounting 階段、updating階段、umounting階段]]
References:
[[@hussainAnswerReactLifecyle2021]]