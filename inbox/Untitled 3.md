## 描述

### useEffect cleanup function

> **為什麼我們從 effect 中回傳一個 function？** 這是 effect 的可選清除機制。每個 effect 都可以回傳一個會在它之後執行清除的 function。這使我們可以把新增和移除 subscription 的邏輯彼此保持靠近。它們都屬於同一個 effect！

> **React 到底什麼時候會清除 effect？** 在 component unmount 時，React 會執行清除。但是，正如我們之前看到的，effect 會在每個 render 中執行，而不僅僅是一次。這是為什麼 React _還_可以在下次執行 effect 之前清除前一個 render 的 effect 的原因。



> before useEffect executes this function the next time / before every new side effect function execution and before the component is removed And it does not run before the first side effect function execution

useEffect cleanup 技術能夠清除掉多出來負責執行side effect的任務，以確保效能不會受損

```
useEffect( () => {
   ....
   return callback
}), [...] )
```


實際會以useEffect 所回傳的callback來定義如何清除多出來的side effect 任務

callback 可以是匿名、箭頭、命名

  

當渲染週期到了且滿足dependency，React 會先透過useEffect 最一開始的callback執行，並取得對應callback，來當作清除用，順序會是

useEffect(callback)-> cleanup = callback(...) -> run cleanup



  

除了第一次side effect 函式之前不會執行以外，在其他下一次side effect執行之前 就清除或者component被移除之前就清除



重點：
- useEffect cleanup 技術主要是確保在下一次side effect 之前就ㄑㄧㄥ



## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: