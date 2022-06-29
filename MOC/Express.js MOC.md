
## 前置知識

- cookie
[[客戶端每當發送請求時，會根據請求的Domain會是什麼而根據cookie上 Domain欄位來添加對應的cookie內容至請求封包]]

## req object
- app.locals 和 req.app.locals
[[app.locals + req.app 兩者一起使用的話，可以進一步讓每一個路徑下的middleware都能使用app.locals變數]]

## middleware

### express-session 
- express-session 安全：
[[Express-session 會替要傳給客戶端當cookie內容的session做簽署以防竄改]]
- express-session 使用
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
[[在沒有任何session的情況下，只要當req.session下任一屬性被寫入，express-session就會為它建立對應的cookie和session]]
[[session的resave功能是盡可能讓潛在可用的session繼續留在session store]]
[[若session的resave關閉後，會依賴著store本身是否具有機制能夠刷新閒置不用的session之過期時間]]
- express-session store:
[[express-session 內建的MemoryStore由於不會監測每個session的狀態來進行記憶體釋放或者管理，所以不適合做真正的session store]]
[[Session 過期時間由session store來規定或者由負責管理和建立的session套件來指定]]

### body-parser
- body-parser
[[body-parser 是express內建套件且 用來解析請求封包下的message body並將解析結果放至req.body]]

- 解析multipart/form-data格式的套件 - multer
[[multer 是一個套件，專門解析multipart中的form-data格式。]]



### 常見問題
- return res.send() vs res.send 問題
[[express - return res.send() vs res.send 問題 ，前者可以中斷目前的執行，後者則是執行完res.send就執行後續]]