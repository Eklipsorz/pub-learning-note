## 描述

讀寫分離(Read/Write Splitting)是指在多個主機擁有同份資料的資料庫的情況下專門提供專門讀取資料的主機和專門寫資料的主機，這些主機都不會是相同的

### 主要解決什麼樣的問題？
1. 資料庫的讀寫壓力會集中於同一個主機或者同一個主機群組，這使得這些主機容易當機、崩潰、不太穩定

### 具體來說的讀寫分離
[[RDS 是一個負責提供關聯式資料庫服務種類，具體會是由N台主機的資料庫服務所構成的大型關聯式資料庫系統服務]]

0.  通常會由一台管理所有擁有資料庫服務的主機的主機負責：
	- 接收請求方對於資料庫的請求
	- 委派請求至實際上的資料庫服務主機
	- 回應處理結果制請求方
![](https://miro.medium.com/max/1400/1*IDQ1KqkHYWwnwtioleYcNw.png)

最後資料庫上的架構會以Master-Slave 架構作為基礎：
1. 由特定主機負責共享自己的資料庫資料給剩下的主機來達成 **多個主機的資料庫共享同一個資料庫資料**，在這情況下，會分配讀取資料權限給一些主機，而寫入權限也給另一部分的主機，讀寫權限賦予的主機都不會相同，爾後客戶端或者使用者若要讀取資料，就去找擁有讀取權限的主機發送讀請求；若要寫入資料，就去找擁有寫入權限的主機發送寫請求

然而讀寫分離下，若擁有寫入權限的主機變多的話，可能會造成資料上不一致，或者需要控管這些主機寫入的執行順序，使他們不會同時寫入同一個值，以造成多個寫權限主機同時執行上的race condition。

2. 常見的實現會以master-slave架構來實現，但並不能夠將read/write splitting和master-slave劃上等號。

3. 在master-slave架構下：擁有讀權限的主機數量若變多的話，會使得master要同步的成本也跟著增加，因爲master主機要多向這一些主機同步同一份資料，然而也會考量由於讀取並不會產生一致性以及主機數越多會增加讀取效率，所以會透過數量變多來平均分攤同一份資料的讀取請求。




#### 實際賦予寫權限的主機數
1. 相對於被賦予讀權限的主機數而言，通常會由少量的主機來被賦予寫權限，常見數量會是1個

#### 實際賦予讀權限
1. 相對於被賦予寫權限的主機數而言，通常會由較多的主機來被賦予讀權限，常見數量會是1個以上，這也包含著master主機

#### 總結：常見讀寫分離的數量
1. 被賦予寫權限的主機數會是1個或者少量，至少會比賦予讀權限的主機還少很多
2. 被賦予讀權限的主機數會是1個以上或者多，至少會比賦予讀權限的主機還多很多

#### 讀寫分離

#### Redis 的讀寫分離
1. 主要會以master-slave結構來實現：由一個master主機負責將資料庫資料共享給多個slave主機，來讓大家共享著同個資料，接著賦予寫權限給master 主機；賦予讀權限給slave 主機


### 讀寫分離的場景
在這裡會以常見讀寫分離的數量為主：
1. 適用於讀請求遠大於寫請求的場景、更新少和查詢多的場景

> 當業務對於資料庫讀與寫的操作數量差距非常大時，為了避免資料庫的寫入影響查詢的效率時，建議採用讀寫分離技術。

> **PS：**資料庫不一定要讀寫分離，如果程序使用資料庫較多時，而更新少，查詢多的情況下會考慮使用，利用資料庫主從同步 ，可以減少資料庫壓力，提高性能。

 >  對於讀操作為主的應用，可以確保寫的伺服器壓力更小，而讀又可以接受點時間上的延遲。  
  

## 複習

#🧠 Read/Write Splitting 架構上通常會誰來負責管理底下具有資料庫服務的主機？ ->->-> `類似RDS的管理主機`
<!--SR:!2023-09-23,226,229-->

#🧠 Read/Write Splitting 架構上，管理多台具有資料庫服務的主機負責什麼業務？ ->->-> `接收請求方對於資料庫的請求、委派請求給具有資料庫服務的主機、回應處理結果至請求方`
<!--SR:!2023-09-22,239,249-->

#🧠 請透過RDS和Read/Write Splitting 來說明這些主機在做什麼？![](https://miro.medium.com/max/1400/1*IDQ1KqkHYWwnwtioleYcNw.png) ->->-> `master主機、slave主機分別為具有資料庫服務的主機，在這裡會由SQL Proxy來管理整體服務的資料庫請求接收和處理請求回應、並且資料庫服務主機在組成master/slave架構，並由master主機負責熱備份資料至slave主機，讓每個主機都有同份資料的資料庫`
<!--SR:!2025-01-01,520,249-->

#🧠 Read/Write Splitting是什麼樣的技術？（提示：請不要將master-slave套用至這，討論不同主機下的共享和如何分配讀寫) ->->-> `讀寫分離(Read/Write Splitting)是指在多個主機共享同個資料庫資料的情況下專門提供專門讀取資料的主機和專門寫資料的主機，這些主機都不會是相同的`
<!--SR:!2025-05-23,645,249-->


#🧠 Read/Write Splitting 主要解決什麼樣的問題？ ->->-> `主要解決資料庫的讀寫壓力會集中於同一個主機或者同一個主機群組，這使得這些主機容易當機、崩潰、不太穩定`
<!--SR:!2023-11-09,314,250-->

#🧠 Read/Write Splitting 的具體實現如何實現共享同份資料的資料庫？ ->->-> `每個主機都有資料庫，由部分主機負責實時同步同份資料庫的資料至剩下其他的主機下的資料庫中`
<!--SR:!2023-09-16,236,249-->


#🧠 Read/Write Splitting 的具體實現上如何在共享同份資料的資料庫來指定讀寫的主機給使用者用？(提示:權限)->->-> `在這情況下，會分配讀取資料權限給一些主機，而寫入權限也給另一部分的主機，讀寫權限賦予的主機都不會相同，爾後客戶端或者使用者若要讀取資料，就去找擁有讀取權限的主機發送讀請求；若要寫入資料，就去找擁有寫入權限的主機發送寫請求`
<!--SR:!2024-12-24,532,230-->

#🧠 Read/Write Splitting 下在面對寫權限主機數量增減問題時，需要考量到什麼樣的問題（提示：一致性和效能) ->->-> `然而讀寫分離下，若擁有寫入權限的主機變多的話，可能會造成資料上不一致，或者需要控管這些主機寫入的執行順序，使他們不會同時寫入同一個值，以造成多個寫權限主機同時執行的race condition；反之，若擁有寫入權限的主機變少的話，會使整體架構的寫入效能變差。`
<!--SR:!2024-03-30,324,229-->


#🧠 Read/Write Splitting 下的讀權限主機數量增減需要考量到什麼樣的主題來決定（提示：含同步成本、帶來的好處) ->->-> `擁有讀權限的主機數量若變多的話，會使得master要同步的成本也跟著增加，因爲master主機要多向這一些主機同步同一份資料，然而也會考量由於讀取並不會產生一致性以及主機數越多會增加讀取效率，所以會透過數量變多來平均分攤同一份資料的讀取請求。若變少的話，需要同步的成本較為低、讀取效率較為低和資料上的完整性和一致性會稍微不足、主機數較少會減少讀取效率`
<!--SR:!2024-12-25,533,249-->



#🧠 Read/Write Splitting ：實際賦予寫權限的主機數 會是？(提示：請拿讀權限的主機數來比較)->->-> `相對於被賦予讀權限的主機數而言，通常會由少量的主機來被賦予寫權限，常見數量會是1個`
<!--SR:!2024-07-22,471,250-->

#🧠 Read/Write Splitting ：實際賦予讀權限的主機數 會是？(提示：請拿寫權限的主機數來比較) ->->-> `相對於被賦予寫權限的主機數而言，通常會由較多的主機來被賦予讀權限，常見數量會是1個以上，這也包含著master主機`
<!--SR:!2024-07-21,471,250-->


#🧠 Read/Write Splitting 的場景為何？ (以1個寫權限主機和多個讀權限主機來說明)->->-> `適用於讀請求遠大於寫請求的場景、更新少和查詢多的場景`
<!--SR:!2024-02-28,240,230-->

---
Status: #🌱 
Tags:
[[Database]]
Links:
[[redis master-slave 架構是 master主機負責對資料做寫入，slave主機負責對資料做存取]]
[[redis sentinel 模式是監測master+slave結構下的所有主機並根據是否故障來調整可用主機給客戶端使用]]
[[race condition 是指多個程式模組以不受控制的執行順序來彼此競爭最後結果，使結果不如開發者所預期的結果]]
[[RDS 是一個負責提供關聯式資料庫服務種類，具體會是由N台主機的資料庫服務所構成的大型關聯式資料庫系統服務]]
[[Master-Slave Replication 是允許一台主要資料庫伺服器將特定資料複製成副本分給多個資料庫系統的資料庫來儲存]]
References:
[[@laowangtanyunweiWeiShiMoZiLiaoKuDuXieFenLiNengTiGaoZiLiaoKuDeXingNeng]]
