## 描述

引用[[@wikidataBeiFen2022]]所描述：
> **溫備份**（Warm Backup）：將備份系統已安裝組態成與當前使用的系統相同或相似的系統和網路執行環境，安裝了應用系統業務定期備份資料。一旦發生災難，直接使用定期備份資料，手工逐筆或自動批次追補孤立資料或將終端使用者透過通訊線路切換到備份系統，恢復業務執行。

引用[[@vitaniumWhatDifferenceHot]]所描述：
> Warm backups are also an option. This is when servers are running, but are not currently in use, or are turned on every now and again to get updates from the server backups. Warm backups are generally used for the mirroring of backups or for the replication of backups.

引用[[@wikidataBeiFen2022]]所描述：
> 溫備份伺服器（warm server）一般都是週期性開機，根據主伺服器內容進行更新，然後關機。經常用溫備份伺服器來進行復制和映象操作。


重點：
- warm backup中的warm指的是使用頻率介於hot和cold之間的程度，而backup則是指備份，合併起來就是指備份頻率介於hot和cold之間的備份
- warm backup的具體實現：備份系統與


### 優點
> 優點：裝置投資較少，通訊環境要求不高
### 缺點
> 缺點：恢復時間長，一般要十幾個小時至數天，資料完整性與一致性較差。



## 複習
#🧠 Question :: ->->-> ``

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