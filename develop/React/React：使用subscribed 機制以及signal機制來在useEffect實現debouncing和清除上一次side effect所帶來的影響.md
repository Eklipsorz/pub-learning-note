## 描述




### useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup?
1. 紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容
2. 紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal
3. 紀錄非同步任務ID並於cleanup移除指定任務的ID


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

#### 潛在問題
1. 該方法只能阻止還沒正式執行的非同步任務，其餘較快執行的非同步任務無法被阻止。

### 使用signal 

1. 使用AbortController API來建立controller 和 signal接收處理物件
2. 將signal 接收處理物件安裝至對應的非同步任務
3. 設定cleanup任務：透過closure來專門對當時建立好的controller發送abort signal給搭載signal接收處理物件來讓它停止執行
4. 設定catch或者try...catch等錯誤攔截

```
useEffect(() => {
      // create a instance which sends a signal
      const controller = new AbortController();
	  const signal = controller.signal
	  
      something(…, signal)
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
          controller.abort()
      } 
}, [deps]) 
```




### AbortController 

  
[[@mdnAbortControllerWebAPIs]]

> The **`AbortController`** interface represents a controller object that allows you to abort one or more Web requests as and when desired.
  

> 建構子

> AbortController.AbortController()
> Creates a new `AbortController` object instance.


> 屬性

> AbortController.signal 
> Returns an AbortSignal object instance, which can be used to communicate with, or to abort, a DOM request.
>


> 方法

> AbortController.abort() 
> Aborts a DOM request before it has completed. This is able to abort fetch requests, consumption of any response bodies, and streams.

重點：
- AbortController interface 是定義一個控制器物件來搭載在支援AbortController介面的非同步任務上，使他們能夠接收外部傳送過來的Abort Signal，收到後就變中斷目前任務
- 屬性、建構式、方法
	- 建構式：回傳AbortController物件
	```
	new AbortController()
	```
	- AbortController 屬性 - signal ：主要是對應AbortController 接收訊號並執行中斷的物件-被稱之為AbortSignal，專門搭載至支援AbortController介面的非同步任務
	- AbortController 方法 - abort：主要是發送abort signal至已搭載同一個Controller 之AbortSignal物件的非同步任務，任務接收到就停止任務，但會是以錯誤形式來回報
```
AbortController.abort()
```
- 目前支援AbortController介面的非同步任務種類有：axios、fetch

  
### 發佈/訂閱模式
  
[[@jlin178JSDesignPattern]]

> 在“JavaScript設計模式與開發實踐”書中是說發佈/訂閱模式又叫做“觀察者模式”，但我查了一下其中好像有些差別，在書中定義了發佈/訂閱模式：


> 物件之間的一對多依賴關係，當一個物件狀態發生改變時，所有依賴於它的物件都得到通知。

  

> 我們可以用現實生活中的例子來說明。當你去買東西的時候，你要的款式沒了，這時候就會跟銷售業務員訂貨，你會留下你的電話讓業務員在貨到的時候打電話給你，而不是你每天都打電話問一下貨到了沒有。這樣的行為就是一種發佈/訂閱模式，實際在網頁上DOM節點綁定事件就是採用這種模式：

> 訊息的傳送者（稱為發布者）不會將訊息直接傳送給特定的接收者（稱為訂閱者）。而是將發布的訊息分為不同的類別，無需了解哪些訂閱者（如果有的話）可能存在。

重點：
-  發佈/訂閱模式：設定關係使物件之間產生一對多依賴關係，當一個物件狀態發生狀態，所有依賴於它的物件都會得到對應通知，並且存取最新內容


## 複習
#🧠 React：請問紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容，能實現什麼樣的cleanup?->->-> `清除上一次side effect所帶來的影響、debouncing`
<!--SR:!2023-09-24,196,249-->

#🧠 React：請問紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal，能實現什麼樣的cleanup?->->-> `清除上一次side effect所帶來的影響、debouncing`
<!--SR:!2023-10-03,201,249-->

#🧠 React：請問紀錄非同步任務ID並於cleanup移除指定任務的ID，能實現什麼樣的cleanup?->->-> `清除上一次side effect所帶來的影響、debouncing`
<!--SR:!2023-09-21,195,249-->


#🧠 React：useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup? 手段有哪些？ ->->-> `紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容、紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal、紀錄非同步任務ID並於cleanup移除指定任務的ID`
<!--SR:!2023-09-23,122,229-->


#🧠 React：useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup？ 其中的 **紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容** 是如何實現的？->->-> `在生成非同步任務前，先分配名為subscribed 的記憶體區塊，並設定為true；非同步任務設定以subscribed 對應內容是否為true來執行任務內容：- 若為true，就執行 - 若為false，就不執行；設定cleanup函式：專門設定當前subscribed對應的記憶體區塊為false的任務`
<!--SR:!2023-10-01,201,249-->


#🧠 React：useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup？ 其中的 **紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容** 是如何設定cleanup程式碼？->->-> `return () => { subscribed = false  } `
<!--SR:!2023-09-17,193,249-->


#🧠 React：useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup？ 其中的 **紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容** 是如何設定以下目標的程式碼 **非同步任務設定以subscribed 對應內容是否為true來執行任務內容** ：- 若為true，就執行 - 若為false，就不執行？->->-> ` something(…).then((….) => { if (subscribed)  /* do side effect */ })	`
<!--SR:!2023-09-26,198,249-->


#🧠 React：useEffect 要如何實現debouncing和清除上一次side effect所帶來的影響所需的cleanup？ 其中的 **紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容** 整體程式碼會是如何呈現？ 請添加分配、非同步任務的產生、建立cleanup->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667809557/blog/react/effect/useEffect/cleanup/promise-useEffect-cleanup-based-on-subscribed_g6nm9m.png)`
<!--SR:!2023-10-27,217,249-->


#🧠 React： 以下為useEffect的實現代碼，請用mount階段來說明他們做了什麼？（務必請說明到記憶體和cleanup)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667809557/blog/react/effect/useEffect/cleanup/promise-useEffect-cleanup-based-on-subscribed_g6nm9m.png)->->-> `mount階段時會是先執行： - 分配新記憶體來存放true，名為subscribed - 生成非同步任務，任務執行以subscribed是否為true來執行 - 建立cleanup任務：專門清除目前subscribed所指向的記憶體區塊
<!--SR:!2024-12-24,473,250-->
`

#🧠 React： 以下為useEffect的實現代碼，請用update階段來說明他們做了什麼？（務必請說明到記憶體和cleanup)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667809557/blog/react/effect/useEffect/cleanup/promise-useEffect-cleanup-based-on-subscribed_g6nm9m.png)->->-> `update 階段會是： - 執行目前所擁有的cleanup，這時的closure和函式內容會是以上一個非同步任務產生時的記憶體區塊情況為主 - 分配新記憶體來存放true，名為subscribed，但會與上一次建立的區塊不同，是一塊全新的內容 - 生成非同步任務，任務執行以subscribed是否為true來執行 - 建立cleanup任務：專門清除目前subscribed所指向的記憶體區塊`
<!--SR:!2023-08-18,177,250-->

#🧠 React： 以下為useEffect的實現代碼，請說明cleanup 函式如何正確執行？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667809557/blog/react/effect/useEffect/cleanup/promise-useEffect-cleanup-based-on-subscribed_g6nm9m.png)->->-> `憑藉著函式物件擁有的closure，該closure會對應著當時非同步任務所採用的記憶體區塊，該記憶體區塊正是決定了非同步任務繼續執行的關鍵，所以只要改變該區塊內容就能讓非同步任務停止繼續執行`
<!--SR:!2023-12-10,209,230-->

#🧠 React useEffect：紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容的潛在問題是什麼？->->-> `該方法只能阻止還沒正式執行的非同步任務，其餘較快執行的非同步任務無法被阻止。`
<!--SR:!2023-09-09,192,250-->

#🧠  React useEffect：紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal ，這方法能完全阻止非同步任務嗎？為什麼？ ->->-> `可以，因可以直接強制中斷`
<!--SR:!2023-09-02,187,250-->

#🧠 React useEffect：紀錄非同步任務會用到的subscribed對應的記憶體區塊並於cleanup設定該區塊內容 ，這方法能完全阻止非同步任務嗎？為什麼？ ->->-> `並不能，該方法只能阻止還沒正式執行的非同步任務，其餘較快執行的非同步任務無法被阻止。`
<!--SR:!2024-07-09,363,250-->

#🧠 React useEffect：紀錄非同步任務ID並於cleanup移除指定任務的ID，這方法能完全阻止非同步任務嗎？為什麼？ ->->-> `可以，因可以直接強制中斷`
<!--SR:!2023-09-02,187,250-->


#🧠 React：紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal，具體方式是什麼？ ->->-> `使用AbortController API來建立controller 和 signal接收處理物件；將signal 接收處理物件安裝至對應的非同步任務；設定cleanup任務：透過closure來專門對當時建立好的controller發送abort signal給搭載signal接收處理物件來讓它停止執行；設定catch或者try...catch等錯誤攔截`
<!--SR:!2024-03-11,301,250-->


#🧠 React：紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal，具體程式碼如何安置signal和發送signal ->->-> `  const controller = new AbortController(); const signal = controller.signal something(…, signal)  return () => { controller.abort() } `
<!--SR:!2023-12-11,146,210-->




#🧠 React：以下為useEffect的實現，請問cleanup中發送的abort如何確保是發送signal至正確的非同步任務上來阻止執行？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667811905/blog/react/effect/useEffect/cleanup/AbortController-useEffect-cleanup_biqlup.png) ->->-> `最主要是透過cleanup的closure來記錄到非同步任務會用到的controller所在的記憶體區塊，這樣子可以致使cleanup能夠正確對當前所產生的非同步任務發送signal來阻止執行`
<!--SR:!2024-07-07,360,250-->

#🧠 React：紀錄安裝至非同步任務上的signal 接收處理器對應的記憶體區塊並於cleanup向著接收處理器發送signal，具體程式碼是什麼？(包含catch/try...catch) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1667811905/blog/react/effect/useEffect/cleanup/AbortController-useEffect-cleanup_biqlup.png)`
<!--SR:!2024-04-15,278,230-->

#🧠  目前支援AbortController介面的非同步任務種類有哪些？ ->->-> `axios、fetch`
<!--SR:!2023-11-28,136,230-->

#🧠 AbortController 方法 - abort 語法是？->->-> `AbortController.abort()`
<!--SR:!2024-08-16,395,250-->

#🧠 JS：AbortController interface 如何建構對應類別的物件？ ->->-> `new AbortController()`
<!--SR:!2024-09-11,414,250-->

#🧠 JS：AbortController interface 的 abort 發送的signal 只有誰才能收到？ ->->-> `已搭載同一個Controller 之AbortSignal物件的非同步任務`
<!--SR:!2024-08-23,396,250-->

#🧠 JS：AbortController interface 的 abort 是什麼？ 得先有什麼才能有abort方法 ->->-> `得先建立AbortController 物件才能有。主要是發送abort signal至已搭載同一個Controller 之AbortSignal物件的非同步任務，任務接收到就停止任務，但會是以錯誤形式來回報`
<!--SR:!2024-07-29,376,250-->

#🧠 JS：AbortController interface 的 signal 是什麼？ 得先有什麼才能有signal ->->-> `得先建立AbortController 物件才能有。這是主要是對應AbortController 接收訊號並執行中斷的物件-被稱之為AbortSignal，專門搭載至支援AbortController介面的非同步任務`
<!--SR:!2023-12-04,91,230-->

#🧠 JS： AbortController interface 是什麼？用途是什麼？ ->->-> `是定義一個控制器物件來搭載在支援AbortController介面的非同步任務上，使他們能夠接收外部傳送過來的Abort Signal，收到後就變中斷目前任務`
<!--SR:!2023-12-28,251,250-->



#🧠 軟體開發方式中，發佈/訂閱模式會是指什麼？ ->->-> `設定關係使物件之間產生一對多依賴關係，當一個物件狀態發生狀態，所有依賴於它的物件都會得到對應通知，並且存取最新內容`
<!--SR:!2024-01-13,182,210-->

#🧠 以AbortController 來發送abort而阻止非同步任務的執行，請問非同步任務會以什麼形式而停止執行？ ->->-> `以接收到錯誤的形式來停止執行`
<!--SR:!2024-01-26,267,249-->


---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：useEffect 所生成的cleanupFn 本身會依賴著closure，藉此來影響每一個非同步任務所存取的記憶體區塊，因cleanupFn所擁有的closure正是對應每一次非同步任務所會使用到的記憶體區塊]]
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
References:
[[@jlin178JSDesignPattern]]
[[@mdnAbortControllerWebAPIs]]