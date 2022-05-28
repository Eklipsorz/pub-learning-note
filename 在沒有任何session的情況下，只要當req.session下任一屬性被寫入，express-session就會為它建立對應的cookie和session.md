## 描述

在沒有任何session的情況下，當伺服器上的req.session下任一屬性被寫入 ，express-session就會為它建立對應的cookie和session

比如：
```
req.session.testid = 12
```

cookie方面，會要求客戶端寫入對應的session id至cookie，以到當下次發送同樣伺服器時，也能夾帶對應session-id的cookie來繼續以上次的session來做後續處理。

session方面，會是建立session物件存放在指定的session store中，等到下次客戶端持著session id來發送請求，伺服器就會從store找到對應的session來輸出至req.session


## 複習

#🧠 express-session在沒有任何session的情況下，若伺服器上的req.session下任一屬性被寫入的話，session和cookie會發生什麼事情？ ->->-> `express-session就會為它建立對應的cookie和session，cookie方面，會要求客戶端寫入對應的session id至cookie，以到當下次發送同樣伺服器時，也能夾帶對應session-id的cookie來繼續以上次的session來做後續處理，session方面，會是建立session物件存放在指定的session store中，等到下次客戶端持著session id來發送請求，伺服器就會從store找到對應的session來輸出至req.session`


---
Status: #🌱 
Tags:
[[Session]] - [[Express]]
Links:
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
References: