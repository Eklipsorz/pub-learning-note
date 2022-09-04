## 描述

移除產品所需要的資料同步為：
- 儲存在緩存和資料庫的購物車：一律刪除，並重新計算總金額
- 儲存在緩存上的productsnap：一律刪除
- 儲存在緩存和資料庫上的庫存資料：跟產品相關的庫存紀錄一律刪除
- 儲存在資料庫的訂單：以order_details來紀錄過去訂單所訂購的產品名稱，並保留刪除前的資訊
 - 更新在資料庫上的user_statistics資訊：
	- 所有曾喜歡被刪除產品的使用者，更新在其紀錄上的like_tally =  like_tally - 1
	- 所有曾評論被刪除產品的使用者，更新在其紀錄上的reply_tally = reply_tally - 原本在留言表格所能找到之對應產品和當前使用者的紀錄筆數
- 儲存在資料庫上的喜歡資料：跟產品相關的喜歡紀錄一律刪除
- 儲存在資料庫上的留言資料：跟產品相關的留言紀錄一律刪除
- 儲存在資料庫上的ownerships資料：跟產品相關的紀錄一律刪除
- 儲存在資料庫上的product_statistics：跟產品相關的product_statisics一律刪除
- 儲存在資料庫上的產品：一律刪除
---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: