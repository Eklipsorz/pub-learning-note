

## 描述

由於connect-redis 目前支持著redis 3.x (client端程式)，所以使用上必須得透過legacyMode讓redis 4.x client 主程式的版本能夠兼容4.x以下的程式碼，以避免版本太低才有的功能和程式碼無法使用，而這可以讓connect-redis支援，除此之外還必須要先讓redis client端程式與redis server進行連接

```
// redis@v4
const { createClient } = require("redis")
let redisClient = createClient({ legacyMode: true })
redisClient.connect().catch(console.error)
```


總結需要做：
- 設定redis套件下的createClient函式(主要回傳client主程式)兼容4.x版本以下的版本的程式碼
```
let redisClient = createClient({ legacyMode: true })
```
- client 主程式與server連線
```
redisClient.connect().catch(console.error)
```

### 若不跟著改的話
若不跟著改的話，會無法讓整個session store正常運作，換言之無法正常儲存session。
### legacyMode
根據[[@NodeRedis2022]]所描述的模式：
> Use legacy mode to preserve the backwards compatibility of commands while still getting access to the updated experience:

重點：
- legacyMode 就是盡可能在維持舊版本才有的功能和程式碼情況下升級，而非整個就是4.x版本，並刪去舊版本才有的功能和程式碼

---
Status: #🌱 
Tags:
[[Redis]]
Links:
[[Express-session 會替要傳給客戶端當cookie內容的session做簽署以防竄改]]
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
References:
[[@NodeRedis2022]]