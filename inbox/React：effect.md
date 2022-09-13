## 描述


### React: effect
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]


side effect 是指除了主要效果以外的額外效果：
- 主要效果會是指元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態
- 額外效果會是指
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663086596/blog/react/effect/react-vs-side-effect_yt8q3n.png)


### effect 使用方法

#### function component
useEffect 語法：

- 第一個引數為callback，這些callback只會在dependencies 改變的時候才執行，而不是在component重新渲染的時候呼叫

> a function that should be executed AFTER every component evaluation IF the specified dependencies changes

-  第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies

> dependencies of this effect - the function only runs if the dependencies changed

  

`useEffect(callback, [dependencies])`

  

可以把 `useEffect` 視為 `componentDidMount`，`componentDidUpdate` 和 `componentWillUnmount` 的組合。


effect 是指side effect

working with (side) effects

managing more Complex State with Reducers

manging App-Wide or Component-Wide State with Context 
->
which is built into React to make sharing state and state updates across component easier



if we would send a http reqest

Then we would send this request whenever this function re-runs.

-> 每當這個函式重複執行，就會發送請求

So for example, whenever this state changes and might sometimes be what you want but definitely not always. And if in response to your http request

  

you for example eventually change some state, you would even create an infinite loop

如果你的http 請求是將回應放在狀態上的setState和state來觸發更新渲染的話，會無限重複呼叫該component的建構件、http請求、狀態更新渲染，

  

而這也是為什麼不能把side effect 直接放在component的render，因為會造成額外的無限迴圈。當然若考量到其他更新的方式，只要 請求放在render部分，就還是會衍生出以下循環

呼叫元件的render -> 請求 -> 請求回應 -> 呼叫元件的render -> 請求 -> 請求回應 -> 呼叫元件的render ......

  

如果在沒使用useEffect的情況下，發送http 請求

因為會造成無限迴圈，所以才額外製造一個hook或者特定執行環境

useEffect() is hook：

1. 基於hook而內建

  





## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References: