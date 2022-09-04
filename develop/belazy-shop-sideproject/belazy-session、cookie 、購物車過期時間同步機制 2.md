


### session 
每一次存取/carts中的任一路徑就刷新session在redis的過期時間

### cookie
每一次存取/carts中的任一路徑就刷新cookie在client的過期時間

### 購物車項目
0. 每一次存取/carts 就刷新所有購物車項目的時間
1. 找到購物車項目下的cartId，符合cartId的session，並依據對應session的過期時間來刷新對應購物車的所有項目之過期時間
2. (從未登入->登入)刷新對應session的所有購物車項目之過期時間



### 刷新過期時間的同步順序

session/cookie  -> 購物車所有項目


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References:
