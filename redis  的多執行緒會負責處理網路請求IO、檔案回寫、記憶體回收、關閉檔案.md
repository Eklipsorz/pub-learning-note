## 描述
[[@MianShiGuanWenRedisShiDanZhiXingXuHuanShiDuoZhiXingXu]]所描述：

### 版本3.0

> Redis 3.0 版本後，主程式中除了主執行緒處理網路 IO 和命令操作外，還有 3 個輔助 BIO 執行緒。這 3 個 BIO 執行緒分別負責處理，檔案關閉、AOF 緩衝資料重新整理到磁碟，以及清理物件這三個任務佇列，從而避免這些任務對主 IO 執行緒的影響。
> Redis 在啟動時，會同時啟動這三個 BIO 執行緒，但是 BIO 執行緒只有在需要執行相關型別後臺任務時才會喚醒，其他時間會休眠等待任務。

![](https://i.iter01.com/images/ad6688b840c91cb804f3c2a21289d2e581484efc2c9d9c421bb9323a8299831f.png)

重點：
- 在Redis 3.x版本中，主執行緒負責處理網路請求IO、處理指令操作
- 除了主執行緒以外，還有三個輔助用的BIO 執行緒來負責以下業務，這些執行緒只有在需要時才會被喚醒，平時都會保持睡眠
	- fsync 執行緒：AOF 緩衝資料重新整理到磁碟
	- close執行緒：檔案關閉
	- 清理回收執行緒：清理物件
- fsync 執行緒、close執行緒、清理回收執行緒是Background I/O (BIO) ，會於背景下執行。

### 無多執行緒的redis版本
根據[[@fijismithyRedisSourceCode]]所描述：
![](https://programmer.ink/images/think/50216a37090eb07355566e7e29242bbd.jpg)

重點：
- 單執行緒下會與客戶端建立連線以及socket來接收對應的指令
- 這些指令會依序放在指令佇列中，redis 主要執行緒會從佇列中取出指令執行並將結果放入緩衝區
- 等到所有指令執行完畢後，就負責按照socket資訊將所有指令的結果回寫至對應client端

### 版本6.0

> 多執行緒是 Redis6.0 推出的一個新特性。正如上面所說 Redis 是核心執行緒負責網路 IO ，命令處理以及寫資料到緩衝，而隨著網路硬體的效能提升，單個主執行緒處理⽹絡請求的速度跟不上底層⽹絡硬體的速度，導致網路 IO 的處理成為了 Redis 的效能瓶頸。

> 而 Redis6.0 就是從單執行緒處理網路請求到多執行緒處理，通過多個 IO 執行緒並⾏處理網路操作提升例項的整體處理效能。需要注意的是對於讀寫命令，Redis 仍然使⽤單執行緒來處理，這是因為繼續使⽤單執行緒執行命令操作，就不⽤為了保證 Lua 指令碼、事務的原⼦性，額外開發多執行緒互斥機制了。


![](https://i.iter01.com/images/366286b2a68f20c755c2692895d9ff3a58719c78e75a4adf43ae2be2f6841850.png)


> 全部流程分為以下 4 階段：

> **階段一：服務端和客⼾端建立 Socket 連線，並分配處理執行緒**

> 當有客⼾端請求和例項建立 Socket 連線時，主執行緒會建立和客戶端的連線，並把 Socket 放入全域性等待佇列中。然後主執行緒通過輪詢方法把 Socket 連線分配給 IO 執行緒。

> **階段二：IO 執行緒讀取並解析請求**

> 主執行緒把 Socket 分配給 IO 執行緒後，會進⼊阻塞狀態等待 IO 執行緒完成客戶端請求讀取和解析。

> **階段三：主執行緒執⾏請求操作**

> IO 執行緒解析完請求後，主執行緒以單執行緒的⽅式執⾏這些命令操作。

> **階段四：IO 執行緒回寫 Socket 和主執行緒清空全域性隊**

> 主執行緒執行完請求操作後，會把需要返回的結果寫入緩衝區。然後，主執行緒會阻塞等待 IO 執行緒把這些結果回寫到 Socket 中，並返回給客戶端。等到 IO 執行緒回寫 Socket 完畢，主執行緒會清空全域性佇列，等待客戶端的後續請求。

重點：
- Redis 原本是由單個執行緒負責網路請求I/O、指令執行，但由於客戶端本身網路硬體上升級，這會使向Redis發送請求速率增加，使得Redis的單個執行緒難以應付
- 為了解決上述問題，Redis在6.0建立多個執行緒來負責處理客戶端網路I/O請求、並解析需要執行指令是什麼，流程會是：
	- 先替負責管理I/O多執行緒的模組建立多個佇列，每一次客戶端向redis伺服器發送請求時，主執行緒就先將該請求的socket放進佇列中。
	- 等到佇列滿的時候或者沒請求的時候，主執行緒就平均分攤給I/O執行緒並由執行緒綁定特定Socket來專門接收其客戶端傳送過來的封包。
	- 接著在I/O執行緒開始解析前，主執行緒會保持等待， I/O執行緒接收到封包內容並解析成指令放置redis的執行佇列中，等到I/O執行緒都解析完畢之就會緩醒主執行緒，redis主執行緒就從執行佇列中取出任務並將結果寫入緩衝區，並且將結果和對應socket 來放入為負責管理I/O多執行緒的模組所建立的多個佇列
	- 等到沒任何內容能夠傳送至佇列，就在根據socket來源將結果分發當初綁定socket的IO執行緒，由這些執行緒按照緩衝區位置和socket回寫至對應的客戶端，接著主執行緒就等待I/O執行緒回寫完畢
	- 寫完就緩醒主執行緒來清空所有佇列(I/O 執行緒的等待佇列、執行佇列)
根據[[@fijismithyRedisSourceCode]]所描述：
![](https://programmer.ink/images/think/50216a37090eb07355566e7e29242bbd.jpg)

Process Description:

> 1. The main thread is responsible for receiving the connection establishment request, obtaining the socket and putting it into the global waiting read processing queue
2. After the main thread handles the read event, it allocates these connections to these IO threads through RR(Round Robin)
3. The main thread is blocked, waiting for the IO thread to read the socket
4. The main thread executes the request command through a single thread, and the request data is read and parsed, but it does not execute
5. The main thread is blocked, waiting for the IO thread to write data back to the socket
6. Unbind and empty the waiting queue

![](https://programmer.ink/images/think/a0d97ae13fed61789fe16adc66babc65.jpg)
### socket 內容
1. 含有請求內容/回應內容、請求方資訊(IP、域名、Port)、回應方資訊(IP、域名、Port)

## 複習
#🧠 無多執行緒的redis版本下，如何處理每個請求的？(提示：請考量socket、queue、緩衝區buffer、回寫) ![](https://programmer.ink/images/think/50216a37090eb07355566e7e29242bbd.jpg)->->-> `- 單執行緒下會與客戶端建立連線以及socket來接收對應的指令 - 這些指令會依序放在指令佇列中，redis 主要執行緒會從佇列中取出指令執行並將結果放入緩衝區 - 等到所有指令執行完畢後，就負責按照socket資訊將所有指令的結果回寫至對應client端`
<!--SR:!2022-06-17,3,250-->

#🧠 多執行緒的redis版本下，如何處理每個請求的？(提示：請考量socket、io執行緒、queue、緩衝區buffer、回寫)  ![](https://programmer.ink/images/think/50216a37090eb07355566e7e29242bbd.jpg)->->-> `- 先替負責管理I/O多執行緒的模組建立多個佇列，每一次客戶端向redis伺服器發送請求時，主執行緒就先將該請求的socket放進佇列中。 - 等到佇列滿的時候或者沒請求的時候，主執行緒就平均分攤給I/O執行緒並由執行緒綁定特定Socket來專門接收其客戶端傳送過來的封包。 - 接著在I/O執行緒開始解析前，主執行緒會保持等待， I/O執行緒接收到封包內容並解析成指令放置redis的執行佇列中，等到I/O執行緒都解析完畢之就會緩醒主執行緒，redis主執行緒就從執行佇列中取出任務並將結果寫入緩衝區，並且將結果和對應socket 來放入為負責管理I/O多執行緒的模組所建立的多個佇列 - 等到沒任何內容能夠傳送至佇列，就在根據socket來源將結果分發當初綁定socket的IO執行緒，由這些執行緒按照緩衝區位置和socket回寫至對應的客戶端，接著主執行緒就等待I/O執行緒回寫完畢 - 寫完就緩醒主執行緒來清空所有佇列(I/O 執行緒的等待佇列、執行佇列)`
<!--SR:!2022-06-15,1,230-->

#🧠 Redis 單執行緒在3.0原本是做什麼用途？->->-> `負責網路請求I/O、解析、指令執行、將結果回寫`
<!--SR:!2022-06-17,3,250-->

#🧠 Redis 單執行緒在6.0 是做什麼用途？->->-> `指令執行、將結果回寫分發給I/O執行緒`
<!--SR:!2022-06-17,3,250-->

#🧠 Redis  多執行緒是用來做什麼？ 比如？->->-> `主要是在不影響主要執行緒的原本設計初衷-不產生race codition情況下來，平攤其執行緒的執行壓力，比如說負責處理檔案關閉、緩衝資料回寫至硬碟、記憶體回收、網路請求I/O`
<!--SR:!2022-06-17,3,250-->

---
Status: #🌱 
Tags:
[[Redis]] - [[Operating System]]
Links:
References:
[[@MianShiGuanWenRedisShiDanZhiXingXuHuanShiDuoZhiXingXu]]
[[@fijismithyRedisSourceCode]]