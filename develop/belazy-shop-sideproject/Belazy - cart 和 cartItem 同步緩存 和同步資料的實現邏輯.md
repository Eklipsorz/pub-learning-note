

## 描述
Belazy - cart 和 cartItem 同步緩存 和同步資料的實現邏輯，在這裡主要分為：
- 未登入就加入產品至購物車，但登入後資料庫無對應的購物車資料
- 未登入還沒加入產品至購物車，但登入後資料庫有對應的購物車資料
- 未登入就加入產品至購物車，但登入後資料庫有對應的購物車資料


這三個主要方向都會調用著syncCacheTask和syncDBTask 作為同步cart 紀錄和cartItem紀錄至緩存和同步cart 紀錄和cartItem紀錄至資料庫



### 負責輸入轉換
參數為一個productHashMap

用途為產出一個template能夠方便同步緩存和資料庫，每一個同步過的紀錄都以新的紀錄為主，也就是說createdAt、updatedAt、refreshAt、dirtyBit都會是新造的

從資料庫取出：
- cart紀錄：id、userId、sum、createdAt、updatedAt
- cartItem 紀錄：cartId、productId、price、quantity、createdAt、updatedAt

cart資料庫紀錄轉換成資料邏輯：
- 新增一個空物件template，其屬性為id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- 以productHashMap屬性值來作為其template，key為每一個cartId
```
key -> {....}
```
- 當要存取的key是對應null，那麼初始值就以作為範例
```
{
	id: currentCartId,
	userId: currentUserId,
	sum：0
	createdAt: new Date(),
	updatedAt: new Date(),
	refreshAt: get new RefreshAt,
	dirtyBit: 0,
	oldId: cart紀錄Id
}
```
並且sum 就根據cart紀錄上的sum來加總
```
template.sum = template.sum + sum
```

- 若當要存取的key是對應template，那麼就忽略建立template並以來進行
```
template.sum = template.sum + sum
```

- 輸出會是一個物件
```
{
	id: ...,
	userId: ...,
	sum：...,
	createdAt: ...,
	updatedAt: ...,
	refreshAt: ...,
	dirtyBit: ...,
	oldId: ...
}
```

### syncCacheTask
1. 只負責專注於將資料同步緩存，一律不碰任何資料庫操作
2. 輸入資料規格：
- cart 紀錄分別有id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- cartItem 紀錄分別有cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt、oldCartId、sequelize 
3.  邏輯為：



### syncDBTask
1. 只負責專注於將資料同步資料庫，一律不碰任何緩存操作




---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[購物車資料同步方案會以客戶端能看到的正確資料為主]]
[[Belazy - 購物車內項目檢查]]
[[Belazy - 購物車內項目刪除時的緩存和資料庫之間同步方案]]
References: