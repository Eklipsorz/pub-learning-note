## 描述


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1660833335/blog/react/life-cycle/life-cycle-react_wzmir9.jpg)


### componentWillUmount

[[@reactReactComponentReact]]
> The `componentWillUnmount` method is called when the component is about to be removed from the DOM.

重點：
- componentWillUmount 主用途為
	- 在對應元件的對應DOM節點要從DOM tree移除之前所要做的事情。
- 預設沒有任何處理內容

做完就就直接移除對應DOM節點

### componentDidMount
[[@reactReactComponentReact]]
> 在一個 component 被 mount（加入 DOM tree 中）後，`componentDidMount()` 會馬上被呼叫

重點
- componentDidMount 主用途為
	- 指定對應元件的實際DOM節點加入至DOM tree之後所要做的事情。
- 預設沒有任何處理內容。

## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-08-23,3,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:

References:
[[@reactReactComponentReact]]