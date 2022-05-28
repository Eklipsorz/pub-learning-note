
## 描述

引用[[@express-sessionExpressjsSessionSimple]]所描述的touch功能

> ### [](https://github.com/expressjs/session#storetouchsid-session-callback)store.touch(sid, session, callback)

> **Recommended**

> This recommended method is used to "touch" a given session given a session ID (`sid`) and session (`session`) object. The `callback` should be called as `callback(error)` once the session has been touched.
> This is primarily used when the store will automatically delete idle sessions and this method is used to signal to the store the given session is active, potentially resetting the idle timer.

resave關閉後的警示：
- 當關閉後，一切就要看實現store的套件是否要實現touch中的callback
- 若沒有的話，那麼建議還是設定resave: true
> How do I know if this is necessary for my store? The best way to know is to check with your store if it implements the `touch` method. If it does, then you can safely set `resave: false`. If it does not implement the `touch` method and your store sets an expiration date on stored sessions, then you likely need `resave: true`.
重點：
- express-session 有提供touch這方法會主動監聽哪些session是活躍的並且可以由第三方實現store的套件來指定當事件發生時該如何處理活躍的session，如下方的callback
```
store.touch(sid, session, callback)
```
- 通常第三方的做法會是重置session的計時，使它不要被舊的時限給移除。


---
Status: #🌱 
Tags:
[[Session]] - [[Express]]
Links:
[[session的resave功能是盡可能讓潛在可用的session繼續留在session store]]
References:
[[@express-sessionExpressjsSessionSimple]]