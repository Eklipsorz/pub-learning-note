## 描述

Productsnap 資訊是由產品名稱和產品圖片所構成，資訊儲存的地點為緩存和資料庫，由於儲存地點是根據快慢來分為兩處，所以本身是需要思考同步策略：
1. 使用write-back 並添加入dirtyBit 和 refreshAt，由於是採用refreshAt，所以每一次對snapshot都會花同樣成本來進行檢查
2. 使用write-through ：當對緩存更新資料，就一併更新資料庫上的資料

在這裡會影響Productsnap的 API 會是 新增、編輯、刪除對應產品：
- 新增、編輯、刪除產品比起購物車項目來說，更改頻率會較為低
- 新增產品：通常會經歷一遍設定，才會開始上市


在這裡根據更改頻率較為低這理由來將productsnap同步策略定為使用write-through，不添加dirtyBit 和 refreshAt，每一次更新都對兩處進行更新：
- 當後台管理員新增產品：於緩存和資料庫上，新增對應productsnap
- 當後台管理員移除產品：於緩存和資料庫上，硬性移除對應productsnap
- 當後台管理員編輯產品：於緩存和資料庫上，編輯對應的productsnap




---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: