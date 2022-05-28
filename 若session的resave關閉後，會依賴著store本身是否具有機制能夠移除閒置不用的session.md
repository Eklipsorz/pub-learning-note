
## 描述

引用[[@express-sessionExpressjsSessionSimple]]所描述的touch功能

> ### [](https://github.com/expressjs/session#storetouchsid-session-callback)store.touch(sid, session, callback)

> **Recommended**

> This recommended method is used to "touch" a given session given a session ID (`sid`) and session (`session`) object. The `callback` should be called as `callback(error)` once the session has been touched.
> This is primarily used when the store will automatically delete idle sessions and this method is used to signal to the store the given session is active, potentially resetting the idle timer.

## 複習




---
Status: 
Tags:
Links:
References:
[[@express-sessionExpressjsSessionSimple]]