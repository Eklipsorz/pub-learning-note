## 描述


登入驗證本身會有
1. session-based authentication
2. token-based authentication


### token-based authentication 概念

0. 將token 視為permission/access的形式之一
1. 客戶端從認證授權用的伺服器上獲取permission/access：
	- 伺服器比對使用者所輸入的credential和資料庫上的credential是否一樣，若一樣就做下一步；若不一樣就不做
	 - 建立permission token 給予客戶端
 2. 客戶端藉由permission/access來向管理資源的伺服器索求資源
	- 客戶端使用token來發送請求索要所保護的資源
	- 伺服器驗證token是否合法，合法就允許使用；不合法不允許使用



### 客戶端從伺服器上獲取permission/access

1. 使用者向客戶端提供credential 
2. 客戶端利用使用者提供的credential 來申請對應的token
3. 伺服器收到就進行驗證: 
	- 若驗證成功的話，就產生token
	- 若驗證失敗的話，就回報錯誤訊息
4. 假如驗證成功的話，就將token 轉發給client


![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-token_crodax.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-token_crodax.png)




###  客戶端藉由permission/access來向伺服器索求資源

1. 客戶端利用上一個階段獲取到的token來向管理資源的伺服器申請受保護的資源
2. 伺服器進行驗證
	- 若驗證成功，就回報資源
	- 若驗證失敗，就回報錯誤訊息
3. 若伺服器驗證成功的話，就將資源回送給客戶端


![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-resource_jx4bxp.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-resource_jx4bxp.png)


## 複習

#🧠 登入驗證的實現方式有哪些？ ->->-> `1. session-based authentication 2. token-based authentication`
<!--SR:!2023-06-08,35,250-->


#🧠 登入驗證的實現方式有1. session-based authentication為主的登入驗證 2. token-based authentication，其中token會用什麼技術來製作？ ->->-> `JWT`
<!--SR:!2023-06-05,97,250-->

#🧠 token-based authentication 的驗證概念為何？ ->->-> `將token 視為permission/access的形式之一，token-base authentication 概念為伺服器比對客戶端所提供的使用者所輸入的credential並產生對應token，接著客戶端使用token來向伺服器索求`
<!--SR:!2023-06-07,32,250-->

#🧠 在token-based authentication 的驗證概念中，甚麼東西會被當成permission/access?   ->->-> `token`
<!--SR:!2023-04-29,10,250-->

#🧠 authentication tokens 概念為token-base authentication 概念為伺服器比對客戶端所提供的使用者所輸入的credential並產生對應token，接著客戶端使用token來向伺服器索求，具體會是？？ ->->-> `1. 客戶端從伺服器上獲取permission/access：	- 伺服器比對使用者所輸入的credential和資料庫上的credential是否一樣，若一樣就做下一步；若不一樣就不做。- 建立permission token 給予客戶端 2. 客戶端藉由permission/access來向伺服器索求：- 客戶端使用token來發送請求索要所保護的資源。 - 伺服器驗證token是否合法，合法就允許使用；不合法不允許使用`
<!--SR:!2023-06-05,30,250-->


#🧠 以JWT為主的token-based authentications 通常需要什麼東西才能讓實現？ ->->-> `secret、hashing algorithm `
<!--SR:!2023-05-01,77,250-->

#🧠 token-based authentication: 客戶端藉由tokens來實現從伺服器上獲取permission/access，具體流程會是什麼？->->-> `1. 使用者向客戶端提供credential  2. 客戶端利用使用者提供的credential 來申請對應的token 3. 伺服器收到就進行驗證:  - 若驗證成功的話，就產生token - 若驗證失敗的話，就回報錯誤訊息 4. 假如驗證成功的話，就將token 轉發給client`
<!--SR:!2023-04-26,7,250-->



#🧠 token-based authentication:  客戶端藉由tokens來實現從伺服器上獲取permission/access，具體流程會是什麼？->->-> `1. 客戶端利用上一個階段獲取到的token來向管理資源的伺服器申請受保護的資源 2. 伺服器進行驗證 - 若驗證成功，就回報資源 - 若驗證失敗，就回報錯誤訊息 3. 若伺服器驗證成功的話，就將資源回送給客戶端`
<!--SR:!2023-06-11,34,250-->



#🧠 token-based authentication:  客戶端從伺服器上獲取permission/access，具體流程會是什麼？畫圖表示 ->->->![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-token_crodax.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-token_crodax.png)
<!--SR:!2023-04-29,10,250-->



#🧠 token-based authentication: 客戶端藉由permission/access來向伺服器索求資源，具體流程會是什麼？畫圖表示 ->->->![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-resource_jx4bxp.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1681637521/blog/authentication/token-based-auth-request-resource_jx4bxp.png)
<!--SR:!2023-05-31,27,250-->


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[登入驗證可使用server-side session來實現，並將請求封包處理內容儲存在session並賦予id至客戶端來當作access，好方便客戶端利用access存取]]
[[登入驗證概念為透過與伺服器間的credential驗證過程來獲取access並利用access來向伺服器索求受保護的資源]]
References:
