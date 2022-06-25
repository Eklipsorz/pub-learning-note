## 描述

編輯產品所需要注意的方向為：
- 更新對應產品的Productsnap
- 更新產品表格的對應產品資料
- 透過productId來更新ownerships表格的對應產品
- 更新order_details上的產品資料
- ~~cart_Items 緩存和資料庫~~ 除了productId以外，基本上沒關聯
- ~~stock 緩存和資料庫~~ 除了productId以外，基本上沒關聯
- ~~product_statistics 資料庫~~ 除了productId以外，基本上沒關聯
- ~~replies 資料庫~~   除了productId以外，基本上沒關聯
-  ~~likes~資料庫~~   除了productId以外，基本上沒關聯


### 更新對應產品的Productsnap
根據productsnap的key 來更新對應產品和圖片
```
product:<productId>
```

productsnap 會有：
- name：產品名稱
- image：圖片

### 更新產品表格的對應產品資料
根據productId和輸入參數來修正對應產品資料

### 透過productId來更新ownerships表格的對應產品
根據productId和新選出來的類別來從category 表格找到對應的類別名稱，並把新對應的類別名稱和productId更新至ownership表格

### 更新order_details上的產品資料
根據productId和新產品名稱來修正對應產品資料

### 流程

輸入參數為
- 產品id
- 產品名稱
- 類別id
- 自介
- 圖片

- 檢測參數：
	- 檢測產品id是否存在？錯誤就不得繼續檢測，正確就從中取得產品資料productData'
	- 檢測產品名稱是否超過30字？ 錯誤就回傳目前填入的資料
	- 檢測產品名稱、產品類別是否為空值？錯誤就回傳目前填入的資料
	- 產品類別是否存在？並獲取對應類別名稱，錯誤就回傳目前填入的資料
	- 產品名稱不得與其他產品名稱重複，但若修改的名稱還是原本的名稱就算通過檢測，其餘錯誤就回傳目前填入的資料
- ~~自介補足檢測：檢測自介是否為空值~~ (系統會直接以""來賦予自介)
- ~~輸入參數和productData'比對哪個資料有更新：(用來減少緩存更新次數和order_details資料庫的更新次數)~~
	- ~~比對輸入圖片欄位是否有填寫 (isFilled = false 沒填寫， isFilled = true 填寫)~~
	- ~~比對輸入名稱是否和現存的名稱一樣~~
	- ~~比對輸入類別ID是否和現存的類別ID一樣~~
	- ~~比對除了圖片欄位以外的輸入欄位值是否與現存的欄位值一樣？~~
- ~~若名稱一樣和圖片欄位沒填寫都一樣，就不更新緩存~~ (由於必須是不重複才能允許更新，所以到達這檢測，肯定都會是不同的名稱，~~否則~~ 就一律以產品名稱、產品圖片來更新緩存紀錄 - productsnap
- ~~若輸入類別ID和現存的類別ID一樣的話~~，那麼就以類別id來更新ownerships表格的對應產品，~~否則就不更新~~
- 以輸入參數來更新一筆product表格下的產品紀錄






#### 註記
- 產品種子資料得要設定產品名稱不得重複的保證


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]
References: