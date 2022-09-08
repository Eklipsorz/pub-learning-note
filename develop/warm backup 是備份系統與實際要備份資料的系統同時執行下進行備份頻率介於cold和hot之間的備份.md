## 描述

引用[[@wikidataBeiFen2022]]所描述：
> **溫備份**（Warm Backup）：將備份系統已安裝組態成與當前使用的系統相同或相似的系統和網路執行環境，安裝了應用系統業務定期備份資料。一旦發生災難，直接使用定期備份資料，手工逐筆或自動批次追補孤立資料或將終端使用者透過通訊線路切換到備份系統，恢復業務執行。

引用[[@vitaniumWhatDifferenceHot]]所描述：
> Warm backups are also an option. This is when servers are running, but are not currently in use, or are turned on every now and again to get updates from the server backups. Warm backups are generally used for the mirroring of backups or for the replication of backups.

引用[[@wikidataBeiFen2022]]所描述：
> 溫備份伺服器（warm server）一般都是週期性開機，根據主伺服器內容進行更新，然後關機。經常用溫備份伺服器來進行復制和映象操作。


重點：
- warm backup中的warm指的是使用頻率介於hot和cold之間的程度，而backup則是指備份，合併起來就是指備份頻率介於hot和cold之間的備份
- warm backup 是什麼樣的技術：warm backup 是備份系統與實際要備份資料的系統同時執行下進行備份頻率介於cold和hot之間的備份
- 若備份系統和實際要備份資料的系統各為一個主機的話，那麼備份系統的主機就會溫備份伺服器(warm server)，通常是週期性開機來備份資料，備份完就關機。


### 優點
> 優點：裝置投資較少，通訊環境要求不高

重點：
- 不需要太高成本來實現或者執行備份系統，但比起cold backup的實現略高
### 缺點
> 缺點：恢復時間長，一般要十幾個小時至數天，資料完整性與一致性較差。

重點：
- 由於備份頻率是介於hot和cold之間，所以資料完整性和一致性都比較差，但比cold backup來得好


## 複習
#🧠  warm backup中的warm是指什麼 ->->-> `warm backup中的warm指的是使用頻率介於hot和cold之間的程度，而backup則是指備份，合併起來就是指備份頻率介於hot和cold之間的備份`
<!--SR:!2023-02-13,158,250-->

#🧠 warm backup 是什麼樣的技術？（提示：備份系統和實際要備份資料系統要如何達成備份) ->->-> `warm backup 是備份系統與實際要備份資料的系統同時執行下進行備份頻率介於cold和hot之間的備份`
<!--SR:!2022-11-06,94,250-->

#🧠 warm backup下的warm server是什麼？->->-> `若備份系統和實際要備份資料的系統各為一個主機的話，那麼備份系統的主機就會溫備份伺服器(warm server)，通常是週期性開機來備份資料，備份完就關機。`
<!--SR:!2022-12-06,113,250-->

#🧠 warm backup的優點是？ ->->-> `不需要太高成本來實現或者執行備份系統，但比起cold backup的實現略高`
<!--SR:!2022-11-04,94,250-->

#🧠 warm backup的缺點是？ ->->-> `由於備份頻率是介於hot和cold之間，所以資料完整性和一致性都比較差，但比cold backup來得好`
<!--SR:!2022-09-25,73,250-->

---
Status: #🌱 
Tags:
[[Backup]] - [[Database]]
Links:
[[hot backup 是指在備份系統與實際要備份資料的系統同時併行下進行實時備份或者頻率高到像實時的備份任務]]
[[cold backup 是指在實際備份資料的系統離線下進行備份]]
[[hot、cold、warm 是強調著資料的使用率，hot是頻繁存取的資料、cold是偶爾存取的資料、warm則是之間]]
References:
[[@wikidataBeiFen2022]]
[[@vitaniumWhatDifferenceHot]]