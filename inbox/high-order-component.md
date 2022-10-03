## 描述

[[@reactHigherOrderComponentsReact]]
> A higher-order component (HOC) is an advanced technique in React for reusing component logic. HOCs are not part of the React API, per se. They are a pattern that emerges from React’s compositional nature.

> Concretely, **a higher-order component is a function that takes a component and returns a new component.**

```
const EnhancedComponent = higherOrderComponent(WrappedComponent);
```

[[@ReactHigherOrder]]
> **Higher Order Component** 指的是在 React 中能夠幫助我們**重複使用程式碼的 React Component**。具體來說 **Higher Order Component 是一個 function，而這個 function 可以把 Component 當作參數傳入，並且回傳一個「增強版」的 Component**。

> -   被當作參數放入的 Component 稱作 **Wrapped Component (ChildComponent)**，因為它是被 HOC 包住的。
> -   Higher-Order Component 又稱作 **Enhanced Component** 或 **Composed Component**，但它其實是 Function。


### high-order 命名緣由



### enhance 命名緣由

### compose 命名緣由



## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@reactHigherOrderComponentsReact]]
[[@ReactHigherOrder]]