## 描述
[[@carlQianTanIModel2018]] 描述：

> ## Blocking I/O
基本上, Linux中大部分的socket都是blocking的. 以下是以UDP為範例的blocking I/O 流程圖(書上寫因為TCP比較複雜, 所以用UDP做範例).

![](https://miro.medium.com/max/1204/1*5uPdSnjRALGMiKAYTUZXcA.png)

> 當user process呼叫了recvfrom這個system call時, kernel就會進入前面提到的I/O之第一階段: 等待資料準備. 就network I/O來說, 大多數情況下, 這個時間點都還沒有資料(datagram)到達, 甚至是可能發生錯誤了(通常是system call被interrupt signal中斷). 這時候user process就會一直處於blocking的狀態, 直到recvfrom回傳準備好的資料, 並將資料從kernel複製至user process的memory, 最後待kernel回傳結果(OK)給user process後, user process才解除blocking的狀態並且繼續運作.

> 從上圖來看, 可以知道所謂的blocking就是在I/O執行的兩個階段都被block住了. 在system歸還process控制權之前, process都不能再做任何的事情.


[[@StudyNotesModels]] 描述：
> `阻塞 (Blocking)`：調用的程序或者應用程式發起請求，在獲得結果之前，調用方的程序會懸 (Hang) 住不動，無法回應，直到獲得結果。


重點：
- Blocking I/O Model 是種 I/O處理模型，縮寫為BIO Model。
- 只要有任務、程序、應用程式發起I/O請求，在獲得結果之前，任務、程序、應用應用程式都會保持等待，直到該I/O請求回應結果，才會解除等待

### Blocking I/O 命名緣由
1. 相對於Non Blocking I/O Model而言，是一種I/O請求會阻塞呼叫一方的模式


## 複習
#🧠 Blocking I/O Model 是什麼樣的概念 ->->-> `是種 I/O處理模型，只要有任務、程序、應用程式發起I/O請求，在獲得結果之前，任務、程序、應用應用程式都會保持等待，直到該I/O請求回應結果，才會解除等待`
<!--SR:!2022-06-17,3,250-->


#🧠 Blocking I/O 命名緣由->->-> `相對於Non Blocking I/O Model而言，是一種I/O請求會阻塞呼叫一方的模式`

---
Status: #🌱 
Tags:
[[I/O handling]] - [[Operating System]]
Links:
References:
[[@carlQianTanIModel2018]]
[[@StudyNotesModels]]