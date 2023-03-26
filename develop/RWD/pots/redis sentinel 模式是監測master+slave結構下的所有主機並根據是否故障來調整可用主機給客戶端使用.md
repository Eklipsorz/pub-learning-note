## 描述

引用[[@wujiannanRedisSentinelJianJieYuBuShu]]所描述：
> 主從模式實現了讀寫分離，並解決了數據備份和單一模式可能引發的效能問題，但其在使用上也有不便之處。因為客戶端連接到不同的 redis instance 時，都得要指定IP端口，若所連接的 instance 故障下線了，主從模式無法通知客戶端切換到另一個可用的 instance，只能靠手動去修改配置並重新取得新的連線。若是故障的是主節點，所有的從節點會因為沒有主節點而同步中斷，進而變成各自獨立的節點，即整個叢集無效，直至手動修改配置或是重啟主節點。

![](https://www.tpisoftware.com/tpu/File/html/202009/20200918141416/images/20200917173700.png)

> 哨兵模式主要執行以下四個任務:
> 1. Monitoring: sentinel 會持續地定期檢查主從節點是否正常運作
> 2. Notification: 當被監控的節點服務出現問題時，sentinel 會透過 API 向管理者或其他相關應用程序發送通知
> 3. Automatic failover: 當主節點未如期工作或無法正常服務時，sentinel 會將失效主節點下的其中一個從節點推選為新的主節點，並設定其他從節點使用新的主節點
> 4. Configuration provider: 為客戶端提供 service discovery，客戶端可以透過 sentinel 取得主節點的連線資訊，包括故障轉移後新的主節點位址

重點：
- sentinel 是以master/slave為基礎來解決其問題-自動監測哪些主機已經故障並試著將可用的主機替代故障主機並分配給客戶端使用，包含master主機、slave主機：
	- 若master主機壞掉的話，sentinel 組鄧從原本master主機下的slave主機找到可用的主機來替代master主機，並由剩下的slave主機來擔任新master主機的slave主機
	- 若slave主機壞掉的話，就自動從剩下可用的slave主機來替代
- 常見的master/slave 本身是redis 常見模式，主要負責解決讀寫分離、資料備份，然而當某個主機因當機或者無法及時處理時，就必須手動調整可用的主機來替代它去為客戶端實現，甚至是若master主機，就必須手動找到可用的master主機來重新構築master/slave

### 單純的master/slave 結構用途是？


### note
1. sentinel：原意為被聘請用來觀察或者注意某個東西的人，在電腦科學裡，是指負責監控某些主機的主機或者實體

> sentine:  **a person employed to guard something**

> guard: **to watch someone and make certain they do not escape from a place**

## 複習
#🧠 redis sentinel 是什麼樣的技術？ ->->-> `sentinel 是以master/slave為基礎來解決其問題-自動監測哪些主機已經故障並試著將可用的主機分配給客戶端使用`
<!--SR:!2024-04-01,405,250-->

#🧠 redis sentinel 主旨是監測master/slave模式下哪些主機可用並自動調整，請問監控哪些主機？->->-> `master主機和slave主機`
<!--SR:!2024-07-01,463,250-->

#🧠 redis sentinel 主旨是監測master/slave模式下哪些主機可用並自動調整？請問若master主機壞掉後，會如何挑選 ->->-> `sentinel 組鄧從原本master主機下的slave主機找到可用的主機來替代master主機，並由剩下的slave主機來擔任新master主機的slave主機`
<!--SR:!2024-06-26,460,250-->

#🧠 redis sentinel 主旨是監測master/slave模式下哪些主機可用並自動調整？請問若slave主機壞掉後，會如何挑選 ->->-> `若slave主機壞掉的話，就自動從剩下可用的slave主機來重組slave主機群和目前的master主機重新構成新的master/slave架構`
<!--SR:!2023-08-12,263,250-->

#🧠 redis 採用 master/slave 主要解決了哪些問題  ->->-> `主要負責解決讀寫分離、資料備份`
<!--SR:!2023-04-29,133,250-->

#🧠 redis：master/slave和讀寫分離，兩者是一樣的嗎？ 為什麼？->->-> `都不一樣，master/slave只是說明多個redis分成master和slave主機，並由master來分享特定副本給其他slave，而讀寫分離只是master/slave的實現之一`
<!--SR:!2023-12-13,270,250-->

#🧠 redis 採用 master/slave模式後，若部分(含master主機和slave主機)主機掛掉的話，該模式如何解決 ->->-> `當某個主機因當機或者無法及時處理時，就必須手動調整可用的主機來替代它去為客戶端實現`
<!--SR:!2023-10-20,305,250-->

#🧠 redis 因 master/slave模式下的哪個缺失而演變成需要redis sentinel 模式  ->->-> `因master/slave模式無法自動根據主機狀態而自動挑選好的主機來替代`
<!--SR:!2024-04-14,412,250-->

---
Status: #🌱 
Tags:
[[Redis]] - [[Redis Sentinel]]
Links:
References:
[[@magezijieRedisGaoKeYongPianNiGuanZheJiao]]
[[@wujiannanRedisSentinelJianJieYuBuShu]]
