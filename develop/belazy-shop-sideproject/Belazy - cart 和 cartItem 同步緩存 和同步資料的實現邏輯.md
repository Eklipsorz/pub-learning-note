

## 描述
Belazy - cart 和 cartItem 同步緩存 和同步資料的實現邏輯，在這裡主要分為：
- 未登入就加入產品至購物車，但登入後資料庫無對應的購物車資料
- 未登入還沒加入產品至購物車，但登入後資料庫有對應的購物車資料
- 未登入就加入產品至購物車，但登入後資料庫有對應的購物車資料


這三個主要方向都會調用著syncCacheTask和syncDBTask 作為同步cart 紀錄和cartItem紀錄至緩存和同步cart 紀錄和cartItem紀錄至資料庫



## 負責輸入轉換
參數為一個productHashMap

用途為產出一個template能夠方便同步緩存和資料庫，每一個同步過的紀錄都以新的紀錄為主，也就是說createdAt、updatedAt、refreshAt、dirtyBit都會是新造的

轉換順序為：
1. 先從資料庫轉換->再從緩存轉換 (若兩者都有資料)
2. 緩存轉換(若只有緩存有資料)
3. 資料庫轉換(若只有資料庫有資料)

### 轉換從資料庫取出的cart紀錄
從資料庫取出：
- cart紀錄：id、userId、sum、createdAt、updatedAt
- cartItem 紀錄：cartId、productId、price、quantity、createdAt、updatedAt

cart資料庫紀錄轉換成資料邏輯：
- 新增一個空物件template，其屬性為id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- 以cartHashMap屬性值來作為其template，其cartHashMap會與緩存共享，key為每一個cartId
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

### 轉換從資料庫取出的cartItem紀錄
從資料庫取出：
- cart紀錄：id、userId、sum、createdAt、updatedAt
- cartItem 紀錄：cartId、productId、price、quantity、createdAt、updatedAt

cartItem資料庫紀錄轉換成資料邏輯：
- 新增一個空物件template，其屬性為cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt、oldCartId、sequelize
- 以ItemsdHashMap屬性值來作為其template，該ItemsHashMap 會與緩存一起共享，key為每一個cartItem上的productId
```
key -> {....}
```
- 當要存取的key是對應null，那麼初始值就以作為範例
```
{
	cartId: currentCartId,
	productId: cartItem紀錄上的productId,
	price: 0,
	quantity: 0,
	createdAt: new Date(),
	updatedAt: new Date(),
	refreshAt: get new RefreshAt,
	dirtyBit: 0,
	oldCartId: cart紀錄Id,
	sequelize: cart紀錄物件
}
```
並且price、quantity 就根據cartItem紀錄上的price、quantity來加總
```
template.price = template.price + price
template.quantity = template.quantity + quantity
```

- 若當要存取的key是對應template，那麼就忽略建立template並以來進行
```
template.price = template.price + price
template.quantity = template.quantity + quantity
```

## 負責輸入緩存轉換
### 轉換從緩存取出的cart紀錄
從緩存取出：
- cart紀錄：id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt
- cartItem 紀錄：cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt

cart緩存紀錄轉換成資料邏輯：
- 新增一個空物件template，其屬性為id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- 以cartHashMap屬性值來作為其template，其cartHashMap會與資料庫共享，key為每一個cartId
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
	oldId: 若是緩存的話，就設定null，表示資料庫沒有共同有的
}
```
並且sum 就根據cart紀錄上的sum來加總
```
template.sum = template.sum + sum
```

- 若當要存取的key是對應template，那麼就忽略建立template並以來進行
```
template.price = template.price + price
template.quantity = template.quantity + quantity
```

### 轉換從緩存取出的cartItem紀錄
從緩存取出：
- cart紀錄：id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt
- cartItem 紀錄：cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt

cartItem緩存紀錄轉換成資料邏輯：
- 新增一個空物件template，其屬性為cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt、oldCartId
- 以ItemsdHashMap屬性值來作為其template，該ItemsHashMap 會與資料庫一起共享，key為每一個cartItem上的productId
```
key -> {....}
```
- 當要存取的key是對應null，那麼初始值就以作為範例
```
{
	cartId: currentCartId,
	productId: cartItem紀錄上的productId,
	price: 0,
	quantity: 0,
	createdAt: new Date(),
	updatedAt: new Date(),
	refreshAt: get new RefreshAt,
	dirtyBit: 0,
	oldCartId: 若是緩存的話，就設定null，表示資料庫沒有共同有的
	sequelize:  若是緩存的話，就設定null，表示資料庫沒有共同有的
}
```
並且price、quantity 就根據cartItem紀錄上的price、quantity來加總
```
template.price = template.price + price
template.quantity = template.quantity + quantity
```

- 若當要存取的key是對應template，那麼就忽略建立template並以來進行
```
template.price = template.price + price
template.quantity = template.quantity + quantity
```


## 轉換的處理

### template 移除屬性問題解法

### syncCacheTask
1. 只負責專注於將資料同步緩存，一律不碰任何資料庫操作
2. 輸入資料規格：
- cart 紀錄分別有id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- cartItem 紀錄分別有cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt、oldCartId、sequelize 
3.  cart 紀錄同步邏輯為：
- 從template建立對應cartKey
- 從template來打造只有id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt這些屬性的物件
- 以上述物件和cartKey來下達hset來更新
- 以對應cartKey來設定過期時間
4. cartItem 紀錄同步邏輯為：
- 從template建立對應cartItemKey
- 從template來打造只有cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt這些屬性的物件
- 以上述物件和cartItemKey來下達hset來更新
- 以對應cartItemKey來設定過期時間



### syncDBTask
1. 只負責專注於將資料同步資料庫，一律不碰任何緩存操作
2. 輸入資料規格：
- cart 紀錄分別有id、userId、sum、createdAt、updatedAt、dirtyBit、refreshAt、oldId
- cartItem 紀錄分別有cartId、productId、price、quantity、createdAt、updatedAt、dirtyBit、refreshAt、oldCartId、sequelize 
3.  cart 紀錄同步邏輯為：
- 從template來檢查是否有oldId，沒有就設定where目標為id，有就設定where目標為oldId
- 從template來打造只有id、userId、sum、createdAt、updatedAt這些屬性的物件
- 以上述物件和更新目標來下達來更新
5. cartItem 紀錄同步邏輯為：
- 從template來檢查是否有oldCartId，沒有就設定where目標為cartId，有就設定where目標為oldCartId
- 從template來打造只有cartId、productId、price、quantity、createdAt、updatedAt這些屬性的物件
- 檢查是否有sequelize，若有的話，就直接拿上述物件和更新目標來透過sequelize更新，否則就透過RedisToolKit.updateDBTask來對上述物件和更新目標來更新


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
[[購物車資料同步方案會以客戶端能看到的正確資料為主]]
[[Belazy - 購物車內項目檢查]]
[[Belazy - 購物車內項目刪除時的緩存和資料庫之間同步方案]]
References: