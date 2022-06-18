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
1. 先透過添加userId至cart紀錄來同步緩存資料
2. 透過目前cartId來取得緩存裡的cartItem紀錄
3. 取得緩存的總計
4. 先透過登入者的ID取得資料庫上的所有cart紀錄，依最接近"現今"的cart紀錄為主，並從中取得cartId
5. 透過cartId來取得資料庫上的總計
6. 透過第一步驟取到的cartId來從cartItem紀錄找到相對應的紀錄
7. 將緩存中的cartItem和資料庫上的cartItem 合併
8. 將緩存中的總計和資料庫上的總計加總
9. 將前兩者結果更新至緩存目前的cartId

---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: