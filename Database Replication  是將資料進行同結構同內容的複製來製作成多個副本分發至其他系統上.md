## 描述


### 什麼是Database Replication
[[@karanpratansinghSystemDesignComplete]]
> Replication is a process that involves sharing information to ensure consistency between redundant resources such as multiple databases, to improve reliability, fault-tolerance, or accessibility.

[[@homuchenSystemDesignQianTanDatabase2021]]
> 顧名思義就是將一份資料，複製成多份，並把它放到不同的機器上， 好像也沒什麼好說的🤪，接著會看看為什麼要做複製，它會帶來什麼好處及壞處， 再看看要如何做到replication，最後看看在RDBMS、NoSQL或是你自己的系統，是怎麼應用這些概念的。

重點：
- 在電腦科學裡，是指將資料進行同結構同內容的複製來製成多個副本並分發至別處，可以分發至資料庫系統、分發至其他主機
- Database replication則是將副本分發給其他資料庫系統，這包含了：
	- 分發給同個主機下的其他資料庫系統
	- 分發給不同主機下的資料庫系統



### 為何要 Database Replication

[[@homuchenSystemDesignQianTanDatabase2021]]
> ## 資料備份
>
> 把一份資料變成多份放到不同的地方，最明顯的好處就是**備份**，當你的機器壞掉，如果硬碟沒壞， 其實重啟之後資料還是在那邊，但就怕你的機器整組壞光光，或是就是硬碟爆了無法再使用， 此時如果資料有複製道別台機器上，就不用怕會有資料的丟失。

> ## 讀取效能
> 
> 資料都在同一台機器時，所有的讀取查詢都必須經由這台機器來完成，一台機器總有他的瓶頸， 一台不行，那你有試過兩台嗎？三台四台五台嗎～
>
> 對於讀取效能的增進，主要有兩個方向，分別是吞吐量(throughput)及延遲時間(latency)。
> -   **read throughput:** 複製了N份，我就有N台機器可以供我查詢拉，平均分散所有的查詢請求到N台機器上， 預期最多就可以有N倍的throughput。
> -   **read latency:** 另外也可以把一些機器放到離user近一點的地方，減少網路封包來回的時間，降低latency，


重點：
- Database Replication 出現的原因是為了
	- 實現資料備份
	- 增加效能上的請求處理吞吐量(throughput)、每個請求的回應時間(latecny)，尤其是讀取效能


### Database Replication 缺點
[[@homuchenSystemDesignQianTanDatabase2021]]
> ## 儲存空間
> 
> 想當然爾，複製了幾份的資料就需要多幾份的磁碟的空間，不過現在硬碟越來越便宜的時代， 應該不是個大問題。

> ## 資料的不一致
> 
> 不一致的主要來源就是兩種: **replication**和**concurrent write**， 試想一下資料如果只有單一來源，那要跟誰不一致呢？反之，因為有了replica， 每份複製要如何保持同步及一致就會是個問題? 會造成什麼consistency的問題， 後面會在陸續討論。


重點：
- Database Replication 缺點為
	- 儲存空間需求大增
	- 資料一致性、完整性、冗余問題，造成原因為：
		- replication：每個副本(replica)要如何與與目前原始資料保持一致
		- 非同步的寫入

### Replication 命名緣由

> the process by which organisms and genetic or other structures make exact copies of themselves

> the production of exact copies of complex molecules, such as DNA molecules, that occurs during growth of living organisms 


重點：
- 製作與特定事物同結構同內容的副本之流程、行為

### Replica

> an exact copy of an object

重點：
- replica 是經由Replication而產出的副本

## 複習


---
Status: #🌱  
Tags:
[[Database]]
Links:
References:
[[@karanpratansinghSystemDesignComplete]]
[[@homuchenSystemDesignQianTanDatabase2021]]
