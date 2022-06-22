## 描述

編輯產品所需要注意的方向為：

![[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]

假設要刪除的產品為product'

### 刪除儲存在緩存和資料庫的購物車
以cartHashMap來紀錄，Map上的key即為每個購物車上的cartId，value為物件
```
{
	past: 扣除前的金額
	removed: 需要扣除的額度
	current: 扣除後的金額
}
```


1. cart_item緩存：遍歷每個cart_item並利用cartHashMap來標記哪些cartId有購買過product'，接著對其value對應的物件寫入removed值(也就是product'總額度)，接著刪去遍歷過的cart_item
2. cart緩存：根據cartHashMap來遍歷所有買過product'的購物車，並對其value對應物件上的past寫入扣除前的金額，然後按照扣除額度來計算扣除後的金額寫入至current( current = past - removed)，若current為0的話(就表示原本購物車就只有被移除的產品，現在產品移除，原本購物車就沒必要留著)，就直接刪除cart緩存物件，大於0就用current更新對應cart緩存物件上的sum。
3. cart_item資料庫：刪除對應product'的紀錄
4. cart資料庫：根據cartHashMap來遍歷所有買過product'的購物車，並檢查current是否為0，為0就刪除對應cart紀錄，大於0就同步sum。

### 刪除儲存在緩存上的productsnap
直接根據product'的id 來刪除對應產品的productsnap

### 刪除儲存在緩存和資料庫上的庫存資料
直接根據product'的id 來刪除對應產品的庫存資料

### 保留order_details上的對應產品資訊
保留order_details上的產品資訊，並且不在資料庫系統安置referential integrity，以避免資料庫系統不允許讓order_details紀錄從product表格找尋已經刪除的產品，取而代之，是以ORM的形式來實現


保留資訊是為了讓客戶能夠在刪除產品的情況下，還能看到自己買了什麼、多少錢
### 更新在資料庫上的user_statistics資訊
-   所有曾喜歡被刪除產品的使用者，更新在其紀錄上的like_tally = like_tally - 1
-   所有曾評論被刪除產品的使用者，更新在其紀錄上的reply_tally = reply_tally - 原本在留言表格所能找到之對應產品和當前使用者的紀錄筆數
```
where: {
	productId,
	userId
}
```

### 刪除儲存在資料庫上的喜歡資料
直接根據product'的id 來刪除對應產品的喜歡資料
### 刪除儲存在資料庫上的留言資料
直接根據product'的id 來刪除對應產品的留言資料

### 刪除儲存在資料庫上的ownerships資料
直接根據product'的id 來刪除對應產品的ownerships資料
### 刪除儲存在資料庫上的product_statistics

直接根據product'的id 來刪除對應產品的product_statistics資料

### 刪除儲存在資料庫上的product表格之資料
    
直接根據product'的id 來刪除對應產品的product資料


### 流程


- 檢測參數：
	- 檢測產品id是否存在？錯誤就不得繼續檢測，正確就從中取得產品資料productData'
-   儲存在緩存和資料庫的購物車：一律刪除，並重新計算總金額
-   儲存在緩存上的productsnap：一律刪除
-   儲存在緩存和資料庫上的庫存資料：跟產品相關的庫存紀錄一律刪除
-   儲存在資料庫的訂單：以order_details來紀錄過去訂單所訂購的產品名稱，並保留刪除前的資訊
-   更新在資料庫上的user_statistics資訊：
    -   所有曾喜歡被刪除產品的使用者，更新在其紀錄上的like_tally = like_tally - 1
    -   所有曾評論被刪除產品的使用者，更新在其紀錄上的reply_tally = reply_tally - 原本在留言表格所能找到之對應產品和當前使用者的紀錄筆數
-   儲存在資料庫上的喜歡資料：跟產品相關的喜歡紀錄一律刪除
-   儲存在資料庫上的留言資料：跟產品相關的留言紀錄一律刪除
-   儲存在資料庫上的ownerships資料：跟產品相關的紀錄一律刪除
-   儲存在資料庫上的product_statistics：跟產品相關的product_statisics一律刪除
-   儲存在資料庫上的產品：一律刪除 




---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]
References: