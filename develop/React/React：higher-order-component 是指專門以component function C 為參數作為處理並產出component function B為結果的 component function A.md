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

![](https://i.imgur.com/1V7ivZi.png)


重點：
- higher-order component 源自於電腦科學中的 higher-order function
- 在JS中，component  本質上會是以名為component function來構成，所以才拿用higher-order function來改名成higher-order component
- higher-order component 指的是一個專門以component C為參數作為處理並產出 component B為結果 的component A 
	- component C 會被稱之為Wrapped Component
	- component B 通常會由HOC改造而成的Component，會叫做Enhanced / Composed Component
	- Component A 則是將身為輸入的Component C進行處理並轉換成Component B的 Component function，被稱之為Higher-order Component

### higher-order 命名緣由

[[@wikidataHigherorderFunction2022]]
源自於電腦科學中的 higher-order function 
> A function that takes one or more functions as an input, and returns a function as a result

重點：
-  一個以函式C作為輸入參數的函式A，其函式A輸出的結果會是另一個函式B，在這裡的函式A、B、C都為函式

## 複習

#🧠 higher-order-component 中的higher-order 命名緣由為何？ ->->-> `源自於higher-order function，該函式一個以函式C作為輸入參數的函式A，其函式A輸出的結果會是另一個函式B，在這裡的函式A、B、C都為函式`
<!--SR:!2025-02-01,508,250-->

#🧠 higher-order function是一個以函式C作為輸入參數的函式A，其函式A輸出的結果會是另一個函式B，請問輸入函式、專門接收函式並處理的函式，輸出的函式結果在結構會是什麼？(函式嗎？)->->-> `都為函式`
<!--SR:!2023-08-01,188,250-->

#🧠 higher-order function是一個以函式C作為輸入參數的函式A，其函式A輸出的結果會是另一個函式B，請問輸入函式、專門接收函式並處理的函式，輸出的函式結果在結構會是什麼？->->-> `都為函式`
<!--SR:!2023-05-18,138,250-->

#🧠 為什麼component 會引入higher-order function呢？->->-> `在JS，component  本質上會是以名為component function來構成，所以才拿用higher-order function來改名成higher-order component`
<!--SR:!2023-06-24,162,250-->

#🧠 higher-order component 會是什麼？ ->->-> `higher-order component 指的是一個專門以component C為參數作為處理並產出 component B為結果 的component A`
<!--SR:!2024-07-19,393,250-->

#🧠 higher-order component 指的是一個專門以component C為參數作為處理並產出 component B為結果 的component A，在這裡的component 在JS程式實現上會是什麼？ ->->-> `函式`
<!--SR:!2023-08-06,191,250-->

#🧠 higher-order component 所產生出的結果是什麼？ ->->-> `另一個被增強過後的component`
<!--SR:!2024-08-22,415,250-->

#🧠 higher-order component 使用什麼作為輸入處理？ ->->-> `使用一個基本的component`
<!--SR:!2024-12-05,478,250-->


---
Status: #🌱  
Tags:
[[React]]
Links:
References:
[[@reactHigherOrderComponentsReact]]
[[@ReactHigherOrder]]
[[@wikidataHigherorderFunction2022]]