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
- useEffect cleanup 技術主要是執行當前side effect之前，清除上一個side effect所產生的影響
- 用途：
	- 確保每一次effect無論跟隨著render執行多少次，都能按照資料正確執行對應effect，不會因過去所產生的side effect給影響
- 執行時機點：
	- 除了第一次side effect函式之前不會執行cleanup以外，在其他下一次side effect執行之前就清除，在這裡的第一次是指該元件的mounting階段所觸發執行的side effect
	- component被unmount前就清除


### cleanup function 設定方法和使用


```
useEffect( () => {
   ....
   return callback
}), [...] )
```

重點：
- 在這裡side effect 任務本身會額外生成非同步任務為主
- 實際會以useEffect 所回傳的callback來定義如何清除目前當前side effect任務
- callback 可以是匿名、箭頭、命名，而callback內容會是實際定義著如何清除多出來的side effect所產生出來的非同步任務。
- 執行順序(side effect + cleanup)：
	- 每個side effect的執行順序會是( cleanup -> side effect )，並不是執行每個side effect後才執行cleanup
	- 第一個side effect前不會執行cleanup

### useEffect + cleanup function 的使用場景為何？

1. effect會產生額外的非同步任務，而cleanup負責清除多出來的非同步任務
2. effect會產生出影響，而cleanup是清除那影響

### useEffect + cleanup function 要實現什麼？
1. 主要實現debouncing效果來在由互動而產生出的大量連續請求之下取出最後最新的請求來處理。
2. 確保每一次執行effect都不會受到上一個effect的影響下而正確執行

### useEffect 的 cleanup function 執行時機


> ### cleanup function 執行時機
> 結合上述範例，cleanup function 執行的時間點有兩個：
> 
> -   要執行下一個 useEffect 的時候，要先清除上一個 effect
> -   component unmount 的時候，會清除 effect

useEffect：cleanup function執行時機：
	- 執行下一個useEffect之前，會執行effect cleanup
	- component 被 unmount前，會執行effect cleanup

## 複習

#🧠 useEffect：cleanup function執行時機是什麼？ ->->-> `	- 執行下一個useEffect之前，會執行effect cleanup - component 被 unmount前，會執行effect cleanup`
<!--SR:!2025-01-29,528,250-->

#🧠 React ：useEffect + cleanup function 要實現什麼？ ->->-> `1. 主要實現debouncing效果來在由互動而產生出的大量連續請求之下取出最後最新的請求來處理。 2. 確保每一次執行effect都不會受到上一個effect的影響下而正確執行`
<!--SR:!2023-08-26,180,250-->

#🧠 React：通常cleanup的內容會是以什麼內容來實現清除/還原 ->->-> `主要會移除上一次side effect所產生的非同步任務`
<!--SR:!2023-09-09,189,250-->

#🧠 React：useEffect cleanup 技術主要是什麼？ ->->-> `清除源自side effect所產生的多餘非同步任務`
<!--SR:!2024-02-20,315,250-->

#🧠 React：useEffect cleanup 技術的目的是什麼？ ->->-> `確保每一次effect無論跟隨著render執行多少次，都能按照資料正確執行對應effect，不會因過去所產生的side effect給影響`
<!--SR:!2023-08-22,178,250-->


#🧠 React：useEffect cleanup 何時執行？ ->->-> `除了mounting 所觸發執行的side effect以外，執行每個side effect之前都會先執行cleanup 以及 component 被unmount前就執行清除`
<!--SR:!2024-11-10,441,250-->


#🧠 React：useEffect cleanup  的執行時機是除了第一次side effect函式之前不會執行cleanup以外，在其他下一次side effect執行之前就清除，那麼第一次side effectc函式是指什麼？  ->->-> `該元件的mounting階段所觸發執行的side effect`
<!--SR:!2025-01-28,528,250-->

#🧠 React：useEffect cleanup 何時執行？mounting 所觸發執行的side effect會不會執行cleanup？ ->->-> `並不會`
<!--SR:!2023-08-07,168,250-->


#🧠 React：useEffect cleanup的使用場景為何？ cleanup又負責做些什麼？->->-> `使用場景為effect會產生額外的非同步任務，而cleanup負責清除多出來的非同步任務、 effect會產生出影響，而cleanup是清除那影響`
<!--SR:!2024-10-17,429,250-->



#🧠 React：useEffect 如何設定cleanup 函式，其函式內容要寫些什麼？ ->->-> `在useEffect(callback, dependencies)當中的callback 定義著回傳特定callback，該callback正是cleanup函式，然後內容會是如何清除多出來的side effect所產生出來的非同步任務`
<!--SR:!2023-09-10,190,250-->



---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[debouncing 在電腦開發實踐的手段，在連續發送事件觸發的場景下，以確保能取得最後的事件觸發資訊的形式來降低請求方和處理方之間的回應速度。]]
References:
[[@megidaWhyYouShould]]
[[@reactShiYongEffectHook]]
