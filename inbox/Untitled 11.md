## 描述

First. Determine how to do side effect Based on Subscribed (: true / false)

```

useEffect(() => {
      let subscribed = true
      
      something(…)
      .then((….) => {
           if (subscribed) 
           /* do side effect */
       })

      return () => {
          subscribed = false
      } 
}, [deps])
```


Second. Determine how to do side effect Based on signal mechanism 

```
useEffect(() => {
      // create a instance which sends a signal
      something(…)
      .catch(error => {
          /*  cancellation * /
          // do something if it receives
          // an error signal

          /*  others error */
          // do error handling
       })
      .then((….) => {
          /* do side effect */
       })
       
      return () => {
          // send error signal with the instance
      } 
}, [deps]) 
```


1.  利用subscribed 是否為true 來決定side effect 是否繼續執行

  

[https://ithelp.ithome.com.tw/m/articles/10203484](https://ithelp.ithome.com.tw/m/articles/10203484)

  

Fetch => signal 

Axios => cancelToken (built in axios)

  

  

物件之間的一對多依賴關係，當一個物件狀態發生改變時，所有依賴於它的物件都得到通知。 

  

  

  

  

signal

An [AbortSignal](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) object instance; allows you to communicate with a fetch request and abort it if desired via an [AbortController](https://developer.mozilla.org/en-US/docs/Web/API/AbortController).

  

  

各家瀏覽器已經開始加入 [AbortController](https://developer.mozilla.org/zh-TW/docs/Web/API/AbortController) 與 [AbortSignal (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) 介面（也就是 Abort API）的實驗性支援，讓 Fetch 和 XHR 這類的操作在完成前可以被中斷。詳情請參閱相關介面的文件

  

  

建構子

[AbortController.AbortController() (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/AbortController/AbortController)

建立一個新的 AbortController 物件實體。

屬性

[AbortController.signal (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/AbortController/signal) Read only

回傳一個 [AbortSignal (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/AbortSignal) 物件實體，可以用來中斷一個 DOM 請求、或是與其溝通。

方法

[AbortController.abort() (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/AbortController/abort)

在一個 DOM 請求完成前中斷他。這可以用來中斷 [fetch 請求 (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/fetch)、對任何 Response Body 的讀取、或是資料流。

  

支援 

Fetch

  

  

  

  

在“JavaScript設計模式與開發實踐”書中是說發佈/訂閱模式又叫做“觀察者模式”，但我查了一下其中好像有些差別，在書中定義了發佈/訂閱模式：

  

  

物件之間的一對多依賴關係，當一個物件狀態發生改變時，所有依賴於它的物件都得到通知。

  

  

我們可以用現實生活中的例子來說明。當你去買東西的時候，你要的款式沒了，這時候就會跟銷售業務員訂貨，你會留下你的電話讓業務員在貨到的時候打電話給你，而不是你每天都打電話問一下貨到了沒有。這樣的行為就是一種發佈/訂閱模式，實際在網頁上DOM節點綁定事件就是採用這種模式：

  

  

訊息的傳送者（稱為發布者）不會將訊息直接傳送給特定的接收者（稱為訂閱者）。而是將發布的訊息分為不同的類別，無需了解哪些訂閱者（如果有的話）可能存在。

## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
References: