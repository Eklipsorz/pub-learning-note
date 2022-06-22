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


1. cart_item緩存：遍歷每個cart_item並利用cartHashMap來標記哪些cartId有購買過product'，接著對其value對應的物件寫入removed值- product'總額度，接著刪去遍歷過的cart_item
2. cart緩存：根據cartHashMap來遍歷所有買過product'的購物車，並對其value對應物件上的past寫入扣除前的金額，然後按照扣除額度來計算扣除後的金額寫入至current，若current為0的話，就直接刪除cart緩存物件，大於0就更新對應cart緩存物件上的sum。
3. cart_item資料庫：刪除對應product'的紀錄
4. cart資料庫：根據cartHashMap來遍歷所有買過product'的購物車，並檢查current是否為0，為0就刪除對應cart紀錄，大於0就同步sum。

### 刪除儲存在緩存上的productsnap


### 刪除儲存在緩存和資料庫上的庫存資料


### 保留order_details上的對應產品資訊

### 更新在資料庫上的user_statistics資訊
-   所有曾喜歡被刪除產品的使用者，更新在其紀錄上的like_tally = like_tally - 1
-   所有曾評論被刪除產品的使用者，更新在其紀錄上的reply_tally = reply_tally - 原本在留言表格所能找到之對應產品和當前使用者的紀錄筆數

### 刪除儲存在資料庫上的喜歡資料

### 刪除儲存在資料庫上的留言資料

### 刪除儲存在資料庫上的ownerships資料

### 刪除儲存在資料庫上的product_statistics

### 刪除儲存在資料庫上的product表格之資料
          


### 流程

輸入參數為
- 產品id
- 產品名稱
- 類別id
- 自介
- 圖片

- 檢測參數：
	- 檢測產品id是否存在？錯誤就不得繼續檢測，正確就從中取得產品資料productData'





#### 註記
- 購物車同步只是單方面呼叫購物車API中刪除產品，到時就按照購物車資料庫記錄是否能在產品表格找到對應產品來移除，時機是每一次流量不高、負載較低的時候。


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]
References: