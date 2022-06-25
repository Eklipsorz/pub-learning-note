## 描述
[[@wikidataDataCleansing2022]] 所描述：
> **Data cleansing** or **data cleaning** is the process of detecting and correcting (or removing) corrupt or inaccurate records from a record set, table, or database and refers to identifying incomplete, incorrect, inaccurate or irrelevant parts of the data and then replacing, modifying, or deleting the dirty or coarse data.[1] Data cleansing may be performed interactively with data wrangling tools, or as batch processing through scripting.

> After cleansing, a data set should be consistent with other similar data sets in the system. The inconsistencies detected or removed may have been originally caused by user entry errors, by corruption in transmission or storage, or by different data dictionary definitions of similar entities in different stores. Data cleaning differs from data validation in that validation almost invariably means data is rejected from the system at entry and is performed at the time of entry, rather than on batches of data.

重點：
- Data Cleansing 是用以偵測資料集合上所有的髒資料並進行清洗，髒資料會是指違反資料完整性、資料一致性的資料，清洗會是將髒資料修正成具備資料完整性、資料一致性的資料
- 清洗手段：首先會偵測所有有問題的資料，接著按下面方案之一來處理
	- 移除有問題的資料
	- 不移除並試著透過取代、修改來將違反資料修正成不違反
- 清洗結果：資料集合上的每筆紀錄都會保持著資料完整性、一致性的特性。
- 負責執行檢測和資料清洗程序的角色會是誰：
	- 資料庫系統
	- 開發者(本身)
	- 專門做Data Cleansing流程的第三方程式

## 複習
#🧠 Database：Data Cleansing 是什麼樣的技術？->->-> `是用以偵測資料集合上所有的髒資料並進行清洗，髒資料會是指違反資料完整性、資料一致性的資料，清洗會是將髒資料修正成具備資料完整性、資料一致性的資料`


#🧠 Database：Data Cleansing 採取什麼樣的手段來修正髒資料？ (提示：先偵測再來處理) ->->-> `首先會偵測所有有問題的資料，接著按下面方案之一來處理 - 移除有問題的資料 - 不移除並試著透過取代、修改來將違反資料修正成不違反`

#🧠 Database：Data Cleansing 清洗髒資料的結果後，資料集合會變成什麼樣子？ ->->-> `清洗結果：資料集合上的每筆紀錄都會保持著資料完整性、一致性的特性。`


#🧠 Database：Data Cleansing 中負責執行檢測和資料清洗程序的角色會是誰？->->-> `資料庫系統、開發者(本身)、專門做Data Cleansing流程的第三方程式`

---
Status: #🌱 
Tags:
[[Database]]
Links:
References:
[[@wikidataDataCleansing2022]]