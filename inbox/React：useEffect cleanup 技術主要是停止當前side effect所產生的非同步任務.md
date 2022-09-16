## 描述

### useEffect cleanup function

[[@megidaWhyYouShould]]
> Cleaning up side effects in React is a way of stopping side effects that do not need to be executed anymore. A common reason why side effects can be irrelevant is when they are unmounted.

> I order food at work, I get home, and the food arrives at work. What do I need the food for anymore? Feels like a waste of money. As a cleanup, I would want to cancel the order before going home if I do not get it.


[[@reactShiYongEffectHook]]
> **為什麼我們從 effect 中回傳一個 function？** 這是 effect 的可選清除機制。每個 effect 都可以回傳一個會在它之後執行清除的 function。這使我們可以把新增和移除 subscription 的邏輯彼此保持靠近。它們都屬於同一個 effect！

> **React 到底什麼時候會清除 effect？** 在 component unmount 時，React 會執行清除。但是，正如我們之前看到的，effect 會在每個 render 中執行，而不僅僅是一次。這是為什麼 React _還_可以在下次執行 effect 之前清除前一個 render 的 effect 的原因。



> before useEffect executes this function the next time / before every new side effect function execution and before the component is removed And it does not run before the first side effect function execution




重點：
- useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務
- 用途：
	- 節省不必要side effect的執行開銷
- 執行時機點：
	- 除了第一次side effect函式之前不會執行cleanup以外，在其他下一次side effect執行之前就清除
	- component被unmount前就清除
- 執行順序(side effect + cleanup)：
	-  每個side effect的執行順序會是( cleanup -> side effect )

### cleanup function 使用方法


```
useEffect( () => {
   ....
   return callback
}), [...] )
```

重點：
- 在這裡side effect 任務本身會額外生成非同步任務為主
- 實際會以useEffect 所回傳的callback來定義如何清除目前當前side effect任務
- callback 可以是匿名、箭頭、命名，而callback內容會是實際定義如何清除多出來的side effect所產生出來的非同步任務。
- useEffect ＋cleanup 執行順序：假如useEffect(callback, dependencies)
```
callback -> cleanup = callback(...) -> run cleanup
```




## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@megidaWhyYouShould]]
[[@reactShiYongEffectHook]]
