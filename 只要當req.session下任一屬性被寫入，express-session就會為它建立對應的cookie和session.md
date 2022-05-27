只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session

比如：
```
req.session.testid = 12
```


---
Status: #🌱 
Tags:
[[Session]]
Links:
References: