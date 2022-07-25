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



重點：
- synchronous 是源自於電信工程的用語，延伸至電腦科學中是形容著任務：
	- 被形容的任務是指每個任務會連接/使用/依賴前面任務，這代表著每個任務A在前面任務完成之前保持等待，直到前面任務完成時才允許任務A執行。
- asynchronous 是源自於電信工程的用語且是synchronous的相反詞，延伸至電腦科學中：
	- 被形容的任務是指每個任務會是獨立且不依賴於任何任務，這代表著每個任務A在前面任務完成之前不會保持等待，並且可以執行自己的任務內容



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




### Synchronisation 命名緣由


[[@mchlAnswerAsynchronousSynchronous2011]] 所描述：
> Indeed, it's one of these cases, where original meaning of the word was subverted and means something different than in popular usage.
> 
> 'Synchronisation' in telecommunication means that receiver signals whenever it is ready to receive messages, and only after this signal the transmitter will start transmitting. When the transmitter is done with the message, it will signal it has finished, so that receiver can now process the received message and do whatever it is supposed to be doing next.

重點：
- synchronisation 是源自於傳送電子訊息/接收電子訊息的通信工程學科
- 在那個學科裡，synhronisation 負責接收電子訊息的主機A會一直為了接收電子訊息而保持等待，直到收到源自於傳送主機B所發過來的電子訊號，主機A才會有所處理。


### Asynchronisation 命名緣由

1. Asynchronisation 是相對於 synchronisation 的相反概念
2. 負責接收電子訊息的主機A不會為了接收訊息而保持等待，會做自己所要做的任務





## 複習
#🧠 synchronous 或者 Synchronisation 命名緣由為何？ ->->-> `synchronisation 是源自於傳送電子訊息/接收電子訊息的通信工程學科，在那個學科裡，synhronisation 負責接收電子訊息的主機A會一直為了接收電子訊息而保持等待，直到收到源自於傳送主機B所發過來的電子訊號，主機A才會有所處理。`

#🧠 asynchronous 或者 Asynchronisation 命名緣由為何？ ->->-> `Asynchronisation 是相對於 synchronisation 的相反概念、負責接收電子訊息的主機A不會為了接收訊息而保持等待，會做自己所要做的任務`

#🧠 synchronous運用至電腦科學裡，會形容什麼？那又會是什麼意思？ ->->-> `延伸至電腦科學中是形容著任務，被形容的任務是指每個任務會連接/使用/依賴前面任務，這代表著每個任務A在前面任務完成之前保持等待，直到前面任務完成時才允許任務A執行。`

#🧠 asynchronous運用至電腦科學裡，會形容什麼？那又會是什麼意思？->->-> `延伸至電腦科學中是被形容的任務是指每個任務會是獨立且不依賴於任何任務，這代表著每個任務A在前面任務完成之前不會保持等待，並且可以執行自己的任務內容`


#🧠 synchronous task 就一定發生在單執行緒嗎？為什麼 ->->-> `不一定，有時多執行緒上所執行的任務會為了等待前面任務的完成而推遲自己的執行，直到前面任務完成，自己才開始執行`

#🧠 asynchronous task 就一定發生在多執行緒嗎？為什麼  ->->-> `不一定，有時單個執行緒上也會發生asynchronous task，任務們不會等待前面任務執行完畢才執行，而是因為實際能執行的執行緒只有一個，所以會因為排程方法而讓每個任務輪流使用執行緒，實際上也符合其定義`

#🧠 synchronous/asynchronous task就一定跟執行緒數量有關嗎？為什麼 ->->-> `不一定，主要要看執行緒所執行的任務是否發生等待前面任務完成才執行的現象`

#🧠 請畫圖描述asynchronous task 在單執行緒和多執行緒的場景 ->->-> `	- 單執行緒：由於每個任務都是獨立的並不等待彼此是否完成就執行，而是任由排程系統讓他們輪流使用CPU執行 - 多執行緒：每個執行緒上所執行的任務都是獨立的，不會等待前面的任務`


#🧠 請畫圖描述synchronous task 在單執行緒和多執行緒的場景 ->->-> `	- 單執行緒：每個任務等待前面任務執行完畢 - 多個執行緒：每個執行緒要執行的任務等待前面任務執行`

#🧠 synchronous request 是什麼？->->-> `當client端發送請求給server端後，client端必須會保持等待直到server端回應請求，而當server端回應請求時，client端會收到請求做下一個執行任務。`

#🧠 asynchronous request 是什麼？ ->->-> `當client端發送請求給server端後，client端不會等待server回應請求而去做下一個執行任務`


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
References:
[[@mchlAnswerAsynchronousSynchronous2011]]
[[@sandamalAnswerAsynchronousSynchronous2011]]