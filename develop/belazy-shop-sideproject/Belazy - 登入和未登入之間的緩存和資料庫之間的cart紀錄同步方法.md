## 描述


判斷緩存有沒有資料：根據目前所使用的cartId來看緩存有沒有對應紀錄
判斷資料庫有沒有資料：~~根據目前所使用的cartId來看資料庫有沒有對應紀錄~~
									     一律根據目前所獲取到的使用者ID來查看資料庫有沒有對應紀錄
### 緩存有資料/資料庫無資料
1. 先透過添加userId至cart紀錄來同步緩存資料
2. 直接將cartItem紀錄和添加後cart紀錄同步至資料庫上的cart紀錄

不用設置緩存上的過期時間，因緩存的過期時間會在操作上設定



### 緩存無資料/資料庫有資料
登入前沒有sessionId

0. 先取得目前所產生的cartId當作newCartId
1. 先透過登入者的ID取得資料庫上的所有cart紀錄，依最接近"現今"的cart紀錄為主，並從中取得cartId來當作oldCartId，在這會獲取cart紀錄
2. 透過oldCartId來從cartItem紀錄找到相對應的紀錄
3.  將符合oldCartId的cart紀錄和cartItem紀錄同步至緩存中的紀錄，其中紀錄會是以newCartId
4.  對緩存上的cart紀錄和cartItem紀錄設定緩存上的過期時間
5. 將存放於資料庫的cart紀錄和cartItem紀錄更改對應的cartId為newCartId





### 緩存和資料庫都有資料

1. 透過目前的cartId 從緩存中取出cart紀錄和cartItem紀錄:
	- cart 紀錄標記為cartCache
	- cartItem 紀錄標記為cartItemCache
2.透過目前的userId 從資料庫取出最近的cart紀錄和cartItem紀錄:
	- cart 紀錄標記為 cartDB
	- cartItem 紀錄標記為 cartItemDB
3. 緩存和資料庫的cart紀錄之間合併，並構成cart合併紀錄
	- cart紀錄的cartId 一率以緩存為主 
	- cart紀錄的sum 一率加總起來 (具體採用在統一合併的函式)
	- cart紀錄的userId 一率以目前登入者為主
4. 緩存和資料庫的cartItem紀錄之間合併，並構成cartItem合併紀錄
	- 建立一個productHashMap
	- 緩存紀錄對productHashMap做標記和加總
	- 資料庫記錄對productHashMap做標記和加總
	

3. 先透過添加userId至cart紀錄來同步緩存資料
4. 透過目前cartId來取得緩存裡的cartItem紀錄
5. 取得緩存的總計
6. 先透過登入者的ID取得資料庫上的所有cart紀錄，依最接近"現今"的cart紀錄為主，並從中取得cartId
7. 透過cartId來取得資料庫上的總計
8. 透過第一步驟取到的cartId來從cartItem紀錄找到相對應的紀錄
9. 將緩存中的cartItem和資料庫上的cartItem 合併
10. 將緩存中的總計和資料庫上的總計加總
11. 將前兩者結果更新至緩存目前的cartId

---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: