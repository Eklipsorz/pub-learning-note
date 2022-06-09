

## 描述

### 購物範例
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654755676/belazy-shop/example/cart-example_wxv0nq.png)

### 購物車所需資料
1. 每個產品的名稱和圖片：
	- 從product table那取出id、name、image
2. 每個產品的庫存量和價格
	- 從stock table那取出productId、price、quantity、restQuantity

### product schema 
product schema inside DB 會是：
- id (productId)
- name
- introduction
- image
- createdAt
- updatedAt

product schema inside Redis 
- key形式會是：
```
product:<productId>
```

- hash value 架構(這部分比stock資料還少更新，比較多的操作是讀取)：
	- id 
	- name
	- image
	- dirtyBit
	- refreshAt



### stock schema
stock schema 會是：
- id (stock id)
- productId
- quantity
- restQuantity
- price
- createdAt
- updatedAt

stock schema inside Redis
- key形式會是：
```
stock:<stockId>
```

- hash value 架構：
	- productId
	- quantity
	- resetQuantity
	- price
	- createdAt
	- updatedAt：由於經常性變動，所以為求方便而紀錄何時更改
	- dirtyBit
	- refreshAT



### product API
除了庫存量以外，所有與產品相關的API皆不能存取和輸出價格和庫存量
### stock API
除了庫存量本身能夠存取和輸出價格和庫存量以外，其餘則不能存取



### 將購物車所需資料放入至緩存



---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: