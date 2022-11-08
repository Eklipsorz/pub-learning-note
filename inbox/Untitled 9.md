## 描述


[[@ithomeDay21UseEffect]]

> 因此嚴格來說， `useEffect` 其實並不是一種 function component 生命週期的 API。雖然說它的執行時機確實與 `componentDidMount` 以及 `componentDidUpdate` 類似（不過其實有些微區別），但它被設計的用途並不是讓你在 React 運作的特定時機來執行一個自定義的 callback ，而是有一種明確的指定用途 — **用來將原始資料同步到 React elements 以外的東西上**。並且在理想上**這個 effect 無論隨著 render 重複執行了多少次，你的程式都應該保持同步且正常運作。**

> 這確實是有點不同於大多數有 class component 經驗開發者所熟悉的 mount / update / unmount 思考模型。因此如果你嘗試把 effect 寫成是否在 component 第一次的 render 而有所行為不同的話，其實是違反了 `useEffect` 本身預期的設計思維。如果我們的執行結果是依賴於「過程」而不是「目的地」的話，我們很容易寫出同步動作有問題的程式碼。


[[@danabramovCompleteGuideUseEffect]]
> While you can `useEffect(fn, [])`, it’s not an exact equivalent. Unlike `componentDidMount`, it will _capture_ props and state. So even inside the callbacks, you’ll see the initial props and state. If you want to see “latest” something, you can write it to a ref. But there’s usually a simpler way to structure the code so that you don’t have to. Keep in mind that the mental model for effects is different from `componentDidMount` and other lifecycles, and trying to find their exact equivalents may confuse you more than help. To get productive, you need to “think in effects”, and their mental model is closer to implementing synchronization than to responding to lifecycle events.


重點：
- useH

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
References:
[[@ithomeDay21UseEffect]]
[[@danabramovCompleteGuideUseEffect]]