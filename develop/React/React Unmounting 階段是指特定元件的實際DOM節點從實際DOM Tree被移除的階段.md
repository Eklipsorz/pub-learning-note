## 描述

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660833335/blog/react/life-cycle/life-cycle-react_wzmir9.jpg)

### 生命週期

Unmounting 階段是指特定元件的實際DOM節點從實際DOM Tree被移除的階段，流程(函式)會有：
- componentWillUnmount


做完流程就會直接從實際DOM Tree移除

### componentWillUmount

[[@reactReactComponentReact]]
> The `componentWillUnmount` method is called when the component is about to be removed from the DOM.

重點：
- componentWillUmount 主用途為
	- 指定在對應元件的對應DOM節點要從DOM tree移除之前所要做的事情。
- 預設沒有任何處理內容

做完就就直接移除對應DOM節點



## 複習
#🧠 React Unmounting 階段是生命週期的一部分？->->-> `對`
<!--SR:!2023-05-17,165,250-->

#🧠 React Unmounting 階段是什麼？->->-> `指特定元件的實際DOM節點從實際DOM Tree被移除的階段`
<!--SR:!2025-02-27,557,250-->

#🧠 React Unmounting 階段會有什麼流程？ ->->-> `componentWillUnmount`
<!--SR:!2023-06-15,185,250-->

#🧠 React Unmounting 階段做完componentWillUnmount就會移除嗎 ->->-> `對`
<!--SR:!2023-12-10,288,250-->

#🧠 React Unmounting 階段的componentWillUnmount是什麼？ 函x->->-> `函式`
<!--SR:!2025-03-15,566,250-->

#🧠 React Unmounting 階段的componentWillUnmount函式是做什麼 ->->-> `指定在對應元件的實際DOM節點要從DOM Tree移除之前所要做的事情`
<!--SR:!2023-06-23,192,250-->


#🧠 React Unmounting 階段的componentWillUnmount函式預設是做什麼 ->->-> `預設沒有任何處理內容`
<!--SR:!2024-01-22,313,250-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React Mounting 階段是對應元件轉換成對應DOM結構插入至目前DOM Tree來渲染]]
[[React updating 階段是歷經過Mounting階段所觸發元件內上的渲染，大致分為三個部分：New props、setState、forceUpdate]]
[[life cycle 在 react component 是指元件從建立成實例並插入至DOM起至該實例的對應DOM被移除期間所會做的變化和處理，大致分為：mounting 階段、updating階段、umounting階段]]
References:
[[@reactReactComponentReact]]