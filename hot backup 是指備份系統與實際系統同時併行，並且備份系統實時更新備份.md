## 描述
引用[[@wikidataBeiFen2022]]所描述：

> -   **熱備份**（Hot Backup）：系統處於正常運轉狀態下的備份。這種情況下，由於系統中的資料可能隨時在更新，備份的資料相對於系統的真實資料可有一定[滯後](https://zh.wikipedia.org/wiki/%E6%BB%9E%E5%90%8E "滯後")。

引用[[@axinReBeiFenWenBeiFenLengBeiFen]]所描述：
> 備份處於聯機狀態，當前應用系統通過高速通訊線路將資料實時傳送到備份系統，保持備份系統與當前應用系統資料的同步；也可定時在備份系統上恢復應用系統的資料。一旦發生災難，不用追補或只需追補很少的孤立資料，備份系統可快速接替生產系統執行，恢復營業。優點：恢復時間短，一般幾十分鐘到數小時，資料完整性與一致性最好，資料丟失可能性最小。缺點：裝置投資大，通訊費用高，通訊環境要求高，平時執行管理較複雜。
> 熱備份伺服器（hot server）時刻處於開機狀態，同主機保持同步。當主機失靈時，可以隨時啟用熱備份伺服器來代替。

 引用[[@vitaniumWhatDifferenceHot]]所描述：
 > A hot backup is performed whilst users are still logged into a system, whereas a cold backup is done with all users offline.

重點：
- hot backup

### 優點
> 優點：恢復時間短，一般幾十分鐘到數小時，資料完整性與一致性最好，資料丟失可能性最小
### 缺點
> 缺點：裝置投資大，通訊費用高，通訊環境要求高，平時執行管理較複雜




## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Backup]] - [[Database]]
Links:
[[hot、cold、warm 用在資料同步上是指資料一致性，hot是最新、cold是較舊、warm是hot和cold之間]]
References:

[[@axinReBeiFenWenBeiFenLengBeiFen]]
[[@wikidataBeiFen2022]]
[[@vitaniumWhatDifferenceHot]]