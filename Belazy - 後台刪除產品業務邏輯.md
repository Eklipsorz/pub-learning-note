## 描述

編輯產品所需要注意的方向為：

![[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]


### 刪除儲存在緩存和資料庫的購物車
根據productsnap的key 來更新對應產品和圖片
```
product:<productId>
```

productsnap 會有：
- name：產品名稱
- image：圖片

### 刪除儲存在緩存上的productsnap


### 刪除儲存在緩存和資料庫上的庫存資料


### 保留order_details上的對應產品資訊

### 更新在資料庫上的user_statistics資訊

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
- 產品種子資料得要設定產品名稱不得重複的保證


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]
References: