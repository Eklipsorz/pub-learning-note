## 描述

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
## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References: