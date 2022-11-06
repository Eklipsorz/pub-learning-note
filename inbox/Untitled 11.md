## 描述



### 使用subscribed(true/false)

1. 在生成非同步任務前，先分配名為subscribed 的記憶體區塊，並設定為true
2. 非同步任務設定以subscribed 對應內容是否為true來執行任務內容：
		- 若為true，就執行
		- 若為false，就不執行
```
      something(…)
      .then((….) => {
           if (subscribed) 
           /* do side effect */
       })	
```
3. 設定cleanup函式：專門設定當前subscribed對應的記憶體區塊為false的任務
```
      return () => {
          subscribed = false
      } 
```

整體內容會是如下
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


#### 執行方式

mount階段時會是先執行：
- 分配新記憶體來存放true，名為subscribed
- 生成非同步任務，任務執行以subscribed是否為true來執行
- 建立cleanup任務：專門清除目前subscribed所指向的記憶體區塊

P.S. 第二步驟和第三步驟所存取的記憶體區塊subscribed會是同一個，而cleanup憑藉著closure來對應到的


update 階段會是：
- 執行目前所擁有的cleanup，這時的closure和函式內容會是以上一個非同步任務產生時的記憶體區塊情況為主
- 分配新記憶體來存放true，名為subscribed，但會與上一次建立的區塊不同，是一塊全新的內容
- 生成非同步任務，任務執行以subscribed是否為true來執行
- 建立cleanup任務：專門清除目前subscribed所指向的記憶體區塊



### 使用signal 



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

  



Fetch => signal 

Axios => cancelToken (built in axios)

  

  

物件之間的一對多依賴關係，當一個物件狀態發生改變時，所有依賴於它的物件都得到通知。 

  

  



### AbortController 

  
[[@mdnAbortControllerWebAPIs]]

> The **`AbortController`** interface represents a controller object that allows you to abort one or more Web requests as and when desired.
  

> 建構子

> AbortController.AbortController()
> 建立一個新的 AbortController 物件實體。


> 屬性

> AbortController.signal 
    回傳一個 AbortSignal (en-US) 物件實體，可以用來中斷一個 DOM 請求、或是與其溝通。

> 方法

> AbortController.abort() 
> 在一個 DOM 請求完成前中斷他。這可以用來中斷 fetch 請求 (en-US)、對任何 Response Body 的讀取、或是資料流。

重點：
- AbortController interfact 是定義一個控制器物件來讓支援AbortController


  

支援 

Fetch

  

  
### 發佈/訂閱模式
  
[[@jlin178JSDesignPattern]]

> 在“JavaScript設計模式與開發實踐”書中是說發佈/訂閱模式又叫做“觀察者模式”，但我查了一下其中好像有些差別，在書中定義了發佈/訂閱模式：


> 物件之間的一對多依賴關係，當一個物件狀態發生改變時，所有依賴於它的物件都得到通知。

  

> 我們可以用現實生活中的例子來說明。當你去買東西的時候，你要的款式沒了，這時候就會跟銷售業務員訂貨，你會留下你的電話讓業務員在貨到的時候打電話給你，而不是你每天都打電話問一下貨到了沒有。這樣的行為就是一種發佈/訂閱模式，實際在網頁上DOM節點綁定事件就是採用這種模式：

> 訊息的傳送者（稱為發布者）不會將訊息直接傳送給特定的接收者（稱為訂閱者）。而是將發布的訊息分為不同的類別，無需了解哪些訂閱者（如果有的話）可能存在。

重點：
-  發佈/訂閱模式：物件之間的一對多依賴關係，當一個物件狀態發生狀態，所有依賴於它的物件都會得到對應通知，並且存取最新內容


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：useEffect 所生成的cleanupFn 本身會依賴著closure，藉此來影響每一個非同步任務所存取的記憶體區塊，因cleanupFn所擁有的closure正是對應每一次非同步任務所會使用到的記憶體區塊]]
References:
[[@jlin178JSDesignPattern]]
[[@mdnAbortControllerWebAPIs]]