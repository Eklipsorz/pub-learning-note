## 描述



[[@sandamalAnswerAsynchronousSynchronous2011]] 所描述：
> synchronous:- when each task connected and depend on the previous task
> 
> asynchronous:- each task independent from others.


[[@bretanaAnswerAsynchronousVs2009]]

> **Synchronous/Asynchronous HAS NOTHING TO DO WITH MULTI-THREADING.**

> Synchronous or _Synchronized_ means "connected", or "dependent" in some way. In other words, two synchronous tasks must be aware of one another, and one task must execute in some way that is dependent on the other, such as wait to start until the other task has completed.  
> 
> Asynchronous means they are totally independent and neither one must consider the other in any way, either in the initiation or in execution.



[[@wikidataTongBu2021]]
> 同步，可以理解為在通信時、函數調用時、協議棧的相鄰層協議交互時等場景下，發信方與收信方、主調與被調等雙方的狀態是否能及時保持狀態一致。如果一方完成一個動作後，另一方立即就修改了自己的狀態。而異步，是指調用方發出請求就立即返回，請求甚至可能還沒到達接收方，比如說放到了某個緩衝區中，等待對方取走或者第三方轉交；而調用結果是通過接收方主動推送，或調用方輪詢來得到。

> 指在一個系統中所發生的事件（event）之間進行協調，在時間上出現一致性與統一化的現象。在系統中進行同步，也被稱為及時（in time）或同步化的（synchronous, in sync）。

 process或者thread synchronization 是指多個process或者thread相互協調執行方式，使他們在特定層面下的結果會是一樣，若一樣的話，則這些process或者thread會是同步的，反之，為非同步。特定層面通常會是每一個process或thread會等待前面的process或thread執行完才執行


重點：
- 從任務等待前面任務、主調用者等待處理方才執行等執行模式，皆為特定執行規則
- process/thread synchronization：多個process/thread相互協調執行方式，使他們在特定層面下的結果會是一樣：
	- 若一樣的話，則這些process/thread會是同步的
	- 若不一樣的話，則這些process/thread會是非同步的

- 特定層面通常意旨為是否滿足於每一個process/thread會等待前面的process/thread執行完才執行
	- 若任務在相互協調後的執行方式是會等待前面任務完成才執行的話，那麼就為同步任務
	- 若任務在相互協調後的執行方式是不會等待前面任務完成才執行的話，那麼就為非同步/異步任務


### synchronous task 發生場景


[[@bretanaAnswerAsynchronousVs2009]] 所描述
> Synchronous (one thread):
```
1 thread ->   |<---A---->||<----B---------->||<------C----->|
```

> Synchronous (multi-threaded):
```
thread A -> |<---A---->|   
                        \  
thread B ------------>   ->|<----B---------->|   
                                              \   
thread C ---------------------------------->   ->|<------C----->| 
```

重點：
- synchronous task 發生在：
	- 單執行緒：每個任務等待前面任務執行完畢
	- 多個執行緒：每個執行緒要執行的任務等待前面任務執行完畢

### asynchronous task 發生場景
[[@bretanaAnswerAsynchronousVs2009]] 所描述
> Asynchronous (one thread):
```
         A-Start ------------------------------------------ A-End   
           | B-Start -----------------------------------------|--- B-End   
           |    |      C-Start ------------------- C-End      |      |   
           |    |       |                           |         |      |
           V    V       V                           V         V      V      
1 thread->|<-A-|<--B---|<-C-|-A-|-C-|--A--|-B-|--C-->|---A---->|--B-->| 
```

> Asynchronous (multi-Threaded):
```
 thread A ->     |<---A---->|
 thread B ----->     |<----B---------->| 
 thread C --------->     |<------C--------->|
```

> -   Start and end points of tasks A, B, C represented by `<`, `>` characters.
> -   CPU time slices represented by vertical bars `|`

重點：
- asynchronous task 發生在：
	- 單執行緒：由於每個任務都是獨立的並不等待彼此是否完成就執行，而是任由排程系統讓他們輪流使用CPU執行
	- 多執行緒：每個執行緒上所執行的任務都是獨立的，不會等待前面的任務

### synchronous/asynchronous 和執行緒的關係

> Technically, the concept of synchronous/asynchronous really **does not have anything to do with threads**. Although, in general, it is unusual to find asynchronous tasks running on the same thread, it is possible, (see below for examples) and it is _common_ to find two or more tasks executing synchronously on _separate_ threads... 
> 
> No, the concept of synchronous/asynchronous has to do _solely_ with whether or not a second or subsequent task can be initiated before the other (first) task has completed, or whether it must wait. That is all. What thread (or threads), or processes, or CPUs, or indeed, what hardware, the task[s] are executed on is not relevant. Indeed, to make this point I have edited the graphics to show this.



兩者皆沒有關係，執行緒的多寡並不會全然決定被執行的任務就是synchronous還是asynchronous，得看這些任務是否等待前面任務完成才執行



### Synchronous Request vs. Asynchronous Request
運用至請求上，會將client端和server當成電信工程的傳送方和接收方。

1. 同步請求，當client端發送請求給server端後，client端必須會保持等待直到server端回應請求，而當server端回應請求時，client端會收到請求做下一個執行任務。

2. 非同步請求，當client端發送請求給server端後，client端不會等待server回應請求而去做下一個執行任務



## 複習

#🧠 process/thread 的 synchronous 或者 Synchronisation 是什麼意思？  ->->-> `多個process/thread相互協調執行方式，使他們在特定層面下的結果會是一樣`
<!--SR:!2024-09-02,406,250-->

#🧠 process/thread 的 asynchronous 或者 Asynchronisation 是什麼意思？  ->->-> `多個process/thread相互協調執行方式，使他們在特定層面下的結果會是不一樣`
<!--SR:!2024-09-01,405,250-->


#🧠  process/thread 的 synchronous 或者 Synchronisation：多個process/thread相互協調執行方式，使他們在特定層面下的結果若會是一樣，就為同步，若為不一樣，就會是非同步， 該電腦科學裡的特定層面則通常是什麼？ ->->-> `是否滿足於每一個process/thread會等待前面的process/thread執行完才執行`
<!--SR:!2023-11-22,91,230-->

#🧠 process/thread 的 asynchronization：特定層面通常意旨為是否滿足於每一個process/thread會等待前面的process/thread執行完才執行，那麼怎麼樣才能稱呼process/thread為同步的？ ->->-> `若任務在相互協調後的執行方式是會等待前面任務完成才執行的話，那麼就為同步任務`
<!--SR:!2023-11-28,89,230-->

#🧠   process/thread 的 asynchronization：特定層面通常意旨為是否滿足於每一個process/thread會等待前面的process/thread執行完才執行，那麼怎麼樣才能稱呼process/thread為非同步/異步的？ ->->-> `若任務在相互協調後的執行方式是不會等待前面任務完成才執行的話，那麼就為非同步/異步任務`
<!--SR:!2024-12-18,472,250-->



#🧠 synchronous task 就一定發生在單執行緒嗎？為什麼 ->->-> `不一定，有時多執行緒上所執行的任務會為了等待前面任務的完成而推遲自己的執行，直到前面任務完成，自己才開始執行`
<!--SR:!2025-01-25,551,250-->

#🧠 asynchronous task 就一定發生在多執行緒嗎？為什麼  ->->-> `不一定，有時單個執行緒上也會發生asynchronous task，任務們不會等待前面任務執行完畢才執行，而是因為實際能執行的執行緒只有一個，所以會因為排程方法而讓每個任務輪流使用執行緒，實際上也符合其定義`
<!--SR:!2024-05-02,391,250-->

#🧠 synchronous/asynchronous task就一定跟執行緒數量有關嗎？為什麼 ->->-> `不一定，主要要看執行緒所執行的任務是否發生等待前面任務完成才執行的現象`
<!--SR:!2023-10-05,263,250-->

#🧠 請畫圖描述asynchronous task 在單執行緒和多執行緒的場景 ->->-> `	- 單執行緒：由於每個任務都是獨立的並不等待彼此是否完成就執行，而是任由排程系統讓他們輪流使用CPU執行 - 多執行緒：每個執行緒上所執行的任務都是獨立的，不會等待前面的任務`
<!--SR:!2024-05-15,399,250-->


#🧠 請畫圖描述synchronous task 在單執行緒和多執行緒的場景 ->->-> `	- 單執行緒：每個任務等待前面任務執行完畢 - 多個執行緒：每個執行緒要執行的任務等待前面任務執行`
<!--SR:!2024-02-26,351,250-->

#🧠 synchronous request 是什麼？->->-> `當client端發送請求給server端後，client端必須會保持等待直到server端回應請求，而當server端回應請求時，client端會收到請求做下一個執行任務。`
<!--SR:!2024-05-24,404,250-->

#🧠 asynchronous request 是什麼？ ->->-> `當client端發送請求給server端後，client端不會等待server回應請求而去做下一個執行任務`
<!--SR:!2024-11-26,518,250-->


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@wikidataTongBu2021]]
[[@mchlAnswerAsynchronousSynchronous2011]]
[[@sandamalAnswerAsynchronousSynchronous2011]]