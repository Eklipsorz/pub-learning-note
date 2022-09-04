## 描述

增加產品所需要注意的方向為：
- 新增Productsnap
- 新增產品紀錄至產品表格
- 新增緩存和資料庫上的庫存紀錄
- 新增產品統計資料-product_statistics
- 新增一筆產品紀錄至ownerships表格


### 新增 Productsnap
當新增產品時，就產生對應的Productsnap

productsnap 會有：
- name：產品名稱
- image：圖片

### 新增產品紀錄至產品表格
接收輸入參數來新增一筆新紀錄至產品表格


### 新增緩存和資料庫上的庫存紀錄
其產品對應的庫存紀錄上的price、quantity、restQuantity皆為0，productId為指定product

緩存對應的key-value pair會是：
- key 形式為
```
stock:<productId>
```
- value 形式為
```
"productId": "1",
"quantity": "0",
"restQuantity": "0",
"price": "0",
"createdAt": ...,
"updatedAt": ....,
"dirtyBit": 0,
"refreshAt": ...,
```


### 新增產品統計資料-product_statistics
product_statistics上新增一筆對應產品的統計紀錄，其liked_tally、replied_tally皆為0


###  新增一筆產品紀錄至ownerships表格
根據輸入參數來寫進新產品紀錄至ownerships表格



### 流程

輸入參數為
- 產品名稱
- 類別id
- 自介
- 圖片

- 檢測參數：
	- 檢測產品名稱是否超過30字？ 錯誤就回傳目前填入的資料
	- 檢測產品名稱、產品類別是否為空值？錯誤就回傳目前填入的資料
	- 產品類別是否存在？並獲取對應類別名稱，錯誤就回傳目前填入的資料
	- 產品名稱不得與其他產品名稱重複，錯誤就回傳目前填入的資料
- ~~自介補足檢測：檢測自介是否為空值~~ (系統會直接以""來賦予自介)
- 以輸入參數來新增一筆產品紀錄，並從中取得產品類別id、產品名稱、產品圖片
- 以類別名稱、類別id來新增一筆產品紀錄至ownerships表格

- 以productId來新增一筆產品統計資料至統計表格，並設定liked_tally、replied_tally皆為0
- 以productId來新增一筆產品庫存至庫存表格，並設定price=0、quantity=0、restQuantity =0
- 以產品id、price=0、quantity=0、restQuantity =0來新增對應緩存紀錄-stock
- 以產品名稱、產品圖片來新增緩存紀錄 - productsnap


#### 註記
- 產品種子資料得要設定產品名稱不得重複的保證


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[Belazy - 移除產品所需要的資料同步，除了訂單會因為本身會包含過去紀錄以外，其餘都一律刪除]]
References: