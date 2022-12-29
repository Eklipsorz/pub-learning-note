## 描述


登入驗證本身會有
1. server-side session為主的登入驗證
2. authentication tokens，如JWT技術



### authentication tokens 概念

1. 客戶端從伺服器上獲取permission/access：
	- 伺服器比對使用者所輸入的credential和資料庫上的credential是否一樣，若一樣就做下一步；若不一樣就不做
	 - 建立permission token 給予客戶端
 2. 客戶端藉由permission/access來向伺服器索求
	- 客戶端使用token來發送請求索要所保護的資源
	- 伺服器驗證token是否合法，合法就允許使用；不合法不允許使用


### 實現所需

1. 伺服器會需要定義secret、hashing algorithm 來產生hashing key



### 客戶端從伺服器上獲取permission/access

1. 客戶端輸入credential 來給伺服器做使用者驗證
2. 伺服器收到就從資料庫取得對應使用者的credential，看是否完全一樣，若一樣就做下一步；不一樣就告知登入失敗
3. 伺服器會產生一個識別字字串，該字串會由credential和hashing 字串構成，hashing 字串是由伺服器的hashing algorithm和伺服器儲存的secret搭配識別用的資料來組合成獨特且不可反解的hash字串。
4. 將識別字字串傳遞至客戶端
5. 客戶端收到就儲存在客戶端的cookie並用domain和path來標記該資料是屬於哪個伺服器和哪個端點。


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1672252937/blog/authentication/authentication-tokens-generate_n3vrxj.png)




###  客戶端藉由permission/access來向伺服器索求

1. 客戶端藉由識別字字串來向伺服器索求受保護的資源。
2. 伺服器收到就會拿識別用的字串和key、hashing algorithm來產生對應hash字串，並比對hash 字串和客戶端的token內存的內容是否一樣，若一樣就表示這token是由伺服器所產生，且未竄改，那麼就做下一步；若不一樣就表示這token不是由伺服器產生，或者被篡改過的，那麼就告知登入失敗。
3. 伺服器將受保護的資源回傳給客戶端


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1672252937/blog/authentication/authentication-tokens-compare_yld5da.png)


## 複習

#🧠 登入驗證的實現方式有哪些？ ->->-> `1. server-side session為主的登入驗證 2. authentication tokens，如JWT技術`
<!--SR:!2023-01-01,3,250-->

#🧠 登入驗證的實現方式有1. server-side session為主的登入驗證 2. authentication tokens，其中後者的案例會是什麼？ ->->-> `JWT`

#🧠 authentication tokens 概念為何？ ->->-> ` authentication tokens 概念為伺服器比對使用者所輸入的credential並產生對應token，接著客戶端使用token來向伺服器索求`

#🧠 authentication tokens 概念為authentication tokens 概念為伺服器比對使用者所輸入的credential並產生對應token，接著客戶端使用token來向伺服器索求，具體會是？？ ->->-> `1. 客戶端從伺服器上獲取permission/access：	- 伺服器比對使用者所輸入的credential和資料庫上的credential是否一樣，若一樣就做下一步；若不一樣就不做。- 建立permission token 給予客戶端 2. 客戶端藉由permission/access來向伺服器索求：- 客戶端使用token來發送請求索要所保護的資源。 - 伺服器驗證token是否合法，合法就允許使用；不合法不允許使用`
<!--SR:!2023-01-01,3,250-->

#🧠 authentication tokens 通常需要什麼東西才能實現？ ->->-> `secret、hashing algorithm `

#🧠 客戶端從伺服器上獲取permission/access，具體流程會是什麼？->->-> `1. 客戶端輸入credential 來給伺服器做使用者驗證 2. 伺服器收到就從資料庫取得對應使用者的credential，看是否完全一樣，若一樣就做下一步；不一樣就告知登入失敗 3. 伺服器會產生一個識別字字串，該字串會由credential和hashing 字串構成，hashing 字串是由伺服器的hashing algorithm和伺服器儲存的secret搭配識別用的資料來組合成獨特且不可反解的hash字串。 4. 將識別字字串傳遞至客戶端 5. 客戶端收到就儲存在客戶端的cookie並用domain和path來標記該資料是屬於哪個伺服器和哪個端點。`
<!--SR:!2023-01-01,3,250-->


#🧠 客戶端從伺服器上獲取permission/access，具體流程會是什麼？畫圖表示 ->->-> ``


#🧠 客戶端藉由permission/access來向伺服器索求，具體流程會是什麼？->->-> `1. 客戶端藉由識別字字串來向伺服器索求受保護的資源。 2. 伺服器收到就會拿識別用的字串和key、hashing algorithm來產生對應hash字串，並比對hash 字串和客戶端的token內存的內容是否一樣，若一樣就表示這token是由伺服器所產生，且未竄改，那麼就做下一步；若不一樣就表示這token不是由伺服器產生，或者被篡改過的，那麼就告知登入失敗。 3. 伺服器將受保護的資源回傳給客戶端`


#🧠 客戶端藉由permission/access來向伺服器索求，具體流程會是什麼？畫圖表示>->->  ``


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[登入驗證可使用server-side session來實現，並將請求封包處理內容儲存在session並賦予id至客戶端來當作access，好方便客戶端利用access存取]]
[[登入驗證概念為透過與伺服器間的credential驗證過程來獲取access並利用access來向伺服器索求受保護的資源]]
References:
