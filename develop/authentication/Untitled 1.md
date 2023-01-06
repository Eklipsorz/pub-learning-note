## 描述


### 後端的任一服務端點是否回傳新id token和refresh token

> returnSecureToken 為 true
> whether or not to return an ID and refresh token
> but it could be true if we want to get a new token in response

考量到服務端點可能會修改到伺服器內部對於特定事物的credential，所以基於credential而製作的token勢必會出現token新舊問題，所以會替端點增加請求封包的參數來指定是否產生新的token和refresh token
## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References: