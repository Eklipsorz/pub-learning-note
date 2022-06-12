
## 描述
引用[[@express-sessionExpressjsSessionSimple]]所描述的resave功能
> Forces the session to be saved back to the session store, even if the session was never modified during the request. Depending on your store this may be necessary, but it can also create race conditions where a client makes two parallel requests to your server and changes made to the session in one request may get overwritten when the other request ends, even if it made no changes (this behavior also depends on what store you're using).

> The default value is `true`, but using the default has been deprecated, as the default will change in the future. Please research into this setting and choose what is appropriate to your use-case. Typically, you'll want `false`.

> How do I know if this is necessary for my store? The best way to know is to check with your store if it implements the `touch` method. If it does, then you can safely set `resave: false`. If it does not implement the `touch` method and your store sets an expiration date on stored sessions, then you likely need `resave: true`.

重點：
- session store本身會為了釋放空間，而清除掉沒在使用的session，通常做法會是替每個session設定過期時間
- resave功能是只要與client進行連線，那伺服器就會根據對應client的session內容重新寫進另一份session至store，最新的session會綁定新的過期時間，舊的session則會因為舊的過期時間而被釋放或者是直接被刪除
- 若resave為true就啟用該功能；反之，若為false就關閉

### 如何釋放閒置sesion
由於express-session與session-store進行分割，express-session管理好自己的業務-管理每個請求下的session和cookie，同時也委託session-store負責管理儲存/釋放session存在session，所以具體來說會依賴著store本身是否具有機制能夠移除閒置不用的session

## 複習

#🧠  session store 如何釋放沒在使用的session？(提示：跟時間有關)->->-> `session store本身會為了釋放空間，而清除掉沒在使用的session，通常做法會是替每個session設定過期時間`
<!--SR:!2022-06-28,19,250-->

#🧠 express-session上的resave機制上目的是什麼 ->->-> `session的resave功能是盡可能讓潛在可用的session繼續留在session store，繼而延續先前處理結果來增加效率`
<!--SR:!2022-06-25,14,230-->

#🧠 express-session上的resave功能是什麼？->->-> ` resave功能是只要與client進行連線，那伺服器就會根據對應client的session內容重新寫進另一份session至store，最新的session會綁定新的過期時間，舊的session則會因為舊的過期時間而被釋放或者是直接被刪除`
<!--SR:!2022-07-09,28,250-->

#🧠 express-session：如何釋放閒置sesion(提示：express-session 和session store是獨立的)->->-> `由於express-session與session-store進行分割，express-session管理好自己的業務-管理整體的session和cookie，同時也委託session-store負責管理儲存/釋放session存在session，所以具體來說會依賴著store本身是否具有機制能夠移除閒置不用的session`
<!--SR:!2022-06-17,5,248-->


---
Status: #🌱 
Tags:
[[Session]] - [[Express]]
Links:
[[Express-Session 讓Express 伺服器能產生和管理對應的cookie和session]]
[[若session的resave關閉後，會依賴著store本身是否具有機制能夠刷新閒置不用的session之過期時間]]
References:
[[@express-sessionExpressjsSessionSimple]]