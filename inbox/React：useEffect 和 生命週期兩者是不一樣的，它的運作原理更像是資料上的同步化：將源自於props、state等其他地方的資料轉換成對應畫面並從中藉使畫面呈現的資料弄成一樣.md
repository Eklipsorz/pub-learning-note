## 描述

### React 文獻：useEffect 和生命週期之間
[[@ithomeDay21UseEffect]]

> 而 `useEffect` 它並不關心這個 effect 流程是在 mount 時還是 update 時執行，也不關心被重複執行了幾次，只要最後從原始資料同步到 effect 的結果是正確的就可以了。

> 因此嚴格來說， `useEffect` 其實並不是一種 function component 生命週期的 API。雖然說它的執行時機確實與 `componentDidMount` 以及 `componentDidUpdate` 類似（不過其實有些微區別），但它被設計的用途並不是讓你在 React 運作的特定時機來執行一個自定義的 callback ，而是有一種明確的指定用途 — **用來將原始資料同步到 React elements 以外的東西上**。並且在理想上**這個 effect 無論隨著 render 重複執行了多少次，你的程式都應該保持同步且正常運作。**

> 這確實是有點不同於大多數有 class component 經驗開發者所熟悉的 mount / update / unmount 思考模型。因此如果你嘗試把 effect 寫成是否在 component 第一次的 render 而有所行為不同的話，其實是違反了 `useEffect` 本身預期的設計思維。如果我們的執行結果是依賴於「過程」而不是「目的地」的話，我們很容易寫出同步動作有問題的程式碼。


> # **useEffect 的核心思考模型整理**

> 我們來將目前為止提及的各種關於 `useEffect` 的觀念做一個整理：

> -   Function component 並沒有提供生命週期的 API，只有 `useEffect` 提供「同步資料到 effect」的用途
> -   `useEffect` 讓你根據目前的資料來同步 React elements（畫面）以外的任何事物與副作用
>-   在一般情況下， `useEffect` 會在每次 component render 且瀏覽器完成 DOM 的更新 & 繪製畫面**之後**才執行，以避免阻塞 component render 的過程 & 瀏覽器繪製畫面的過程
    -   例外情況：在 React 18 中，如果某次 render 是被 `flushSync` 包著的 `setState` 所觸發，則該次 render 的 effect 將提早在瀏覽器畫面排版與繪製「**之前**」就進行觸發
> -   `useEffect` 在概念上並不區分 mount 與 update 的情況，它們被視為是同一種情境
> -   預設情況下，每一次 render 後都應該執行屬於該 render 的 `useEffect`，來確保同步的正確性與完整性
> -   理想上同一個 effect 無論隨著 render 重複被執行了多少次，你的程式都應該保持同步且正常運作
> -   `useEffect` 的 dependencies 是一種「忽略某些不必要的執行」的效能最佳化手段，而不是用來控制 effect 發生在特定的 component 生命週期，或特定的商業邏輯時機



重點：
- useEffect 本身並不是class based componen上的生命週期上之API，更別說是不是語法糖
- useEffect 和 生命週期兩者是不一樣的，只是useEffect 部分特性與生命週期重疊
- 開發策略也不同，useEffect 是以目標為導向，定義一個callback、deps、會用到的資料來告知React的render完畢之後要做些什麼；後者則是以過程為導向來指定每個階段要做什麼。


### React 官方文獻：useEffect 和生命週期之間

[[@danabramovCompleteGuideUseEffect]]
> While you can `useEffect(fn, [])`, it’s not an exact equivalent. Unlike `componentDidMount`, it will _capture_ props and state. So even inside the callbacks, you’ll see the initial props and state. If you want to see “latest” something, you can write it to a ref. But there’s usually a simpler way to structure the code so that you don’t have to. Keep in mind that the mental model for effects is different from `componentDidMount` and other lifecycles, and trying to find their exact equivalents may confuse you more than help. To get productive, you need to “think in effects”, and their mental model is closer to implementing synchronization than to responding to lifecycle events.


> **React synchronizes the DOM according to our current props and state.** There is no distinction between a “mount” or an “update” when rendering.


重點：
- useEffect 的 運作原理 和 生命週期函式(componentDidMount、componentDidUpdate、componentWillUnmount)的運作原理是不一樣的
- useEffect 的運作原理更像是資料上的同步化(Data Synchronization / Data Synchronize)，但不是絕對一樣：將render會用到的資料同步到effect來處理
[[process synchronization 是指多個任務相互協調執行方式，使他們在特定層面下的結果會是一樣；data synchronization是多個 data 處理相互協調資料如何處理，使他們在特定層面下的結果會是一樣]]
- Data Synchronization 是將源自於props、state等其他地方的資料和畫面上的資料弄成弄成一樣的過程，換言之
	- Data Synchronization 將源自於props、state等其他地方的資料轉換成對應畫面，使畫面呈現的資料弄成一樣的過程
	- Synchronize ：將源自於props、state等其他地方的資料轉換成對應畫面並從中藉使畫面呈現的資料弄成一樣


### useEffect vs. 生命週期函式 差別

1. 運作原理：前者只是單方面在render完畢之後執行什麼；後者則是按照元件的mounting、updating、unmount階段來執行對應內容
2. 開發策略：將會用到的資料、callback、deps來告知React的render完畢之後要做些什麼，後者則是以過程為導向來指定每個階段要做什麼`


## 複習

#🧠 React useEffect 的運作原理和生命週期函式之間的差別是？ ->->-> `1. 運作原理：前者只是單方面在render完畢之後執行什麼；後者則是按照元件的mounting、updating、unmount階段來執行對應內容 2. 開發策略：將會用到的資料、callback、deps來告知React的render完畢之後要做些什麼，後者則是以過程為導向來指定每個階段要做什麼`
<!--SR:!2022-11-21,10,250-->


#🧠 React useEffect 的運作原理和生命週期函式之間的差別是？以運作原理來說的話 ->->-> `前者只是單方面在render完畢之後執行什麼；後者則是按照元件的mounting、updating、unmount階段來執行對應內容`
<!--SR:!2022-11-21,10,250-->

#🧠 React useEffect 的運作原理和生命週期函式之間的差別是？以開發策略來說的話 ->->-> `將會用到的資料、callback、deps來告知React的render完畢之後要做些什麼，後者則是以過程為導向來指定每個階段要做什麼`
<!--SR:!2022-11-19,6,230-->

#🧠 React useEffect 的運作原理比較像什麼？ 拿生命週期和Data Synchronization來比的話，為什麼？(請說明到資料內容是否一樣)->->-> `會更偏向於Data Synchronization，原因在於它會將render會用到的資料納入至render之後的effect來執行，也就是資料從props、state轉移至effect模組，並且兩者內容會是一樣的`
<!--SR:!2022-11-20,9,250-->

#🧠 useEffect 的運作原理比較像什麼？ 拿生命週期和Data Synchronization來比的話，為什麼？->->-> `會更偏向於Data Synchronization，原因在於它會將render會用到的資料納入至render之後的effect來執行，也就是資料從props、state轉移至effect模組，並且兩者內容會是一樣的`
<!--SR:!2022-11-21,10,250-->


#🧠 在React上的Data Synchronization會是指什麼？ ->->-> ` 將源自於props、state等其他地方的資料轉換成對應畫面，使畫面呈現的資料弄成一樣的過程`
<!--SR:!2022-11-20,10,250-->

#🧠 在React上的Data Synchronize會是指什麼？ ->->-> `將源自於props、state等其他地方的資料轉換成對應畫面並從中藉使畫面呈現的資料弄成一樣`
<!--SR:!2022-12-05,18,250-->



---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[process synchronization 是指多個任務相互協調執行方式，使他們在特定層面下的結果會是一樣；data synchronization是多個 data 處理相互協調資料如何處理，使他們在特定層面下的結果會是一樣]]
References:
[[@ithomeDay21UseEffect]]
[[@danabramovCompleteGuideUseEffect]]