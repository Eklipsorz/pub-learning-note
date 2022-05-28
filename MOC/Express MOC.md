
## 前置知識

- cookie
[[客戶端每當發送請求時，會根據請求的Domain會是什麼而根據cookie上 Domain欄位來添加對應的cookie內容至請求封包]]

## middleware
- express-session
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
[[Express-session 會替要傳給客戶端當cookie內容的session做簽署以防竄改]]
[[在沒有任何session的情況下，只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session]]
[[session的resave功能是盡可能讓潛在可用的session繼續留在session store]]
[[若session的resave關閉後，會依賴著store本身是否具有機制能夠移除閒置不用的session]]

- body-parser
[[body-parser 是express內建套件且 用來解析請求封包下的message body並將解析結果放至req.body]]


