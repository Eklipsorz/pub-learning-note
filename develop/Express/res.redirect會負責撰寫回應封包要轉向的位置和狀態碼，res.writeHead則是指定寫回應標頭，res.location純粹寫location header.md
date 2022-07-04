## 描述

 [[@expressExpressAPICanZhao]] 所描述：
 
> ### res.location(path)
> Sets the response `Location` HTTP header to the specified `path` parameter.



> ### res.redirect([status,] path)
> Redirects to the URL derived from the specified `path`, with specified `status`, a positive integer that corresponds to an [HTTP status code](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) . If not specified, `status` defaults to “302 “Found”.


[[@node.jsHTTPNodeJs]]所描述
> res.writeHead(...)
> Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers. Optionally one can give a human-readable `statusMessage` as the second argument.

重點：
- res.location 是直接設定回應封包內的location標頭
- res.redirect 是直接設定回應封包內的location標頭和狀態碼
- res.writeHead 是直接設定回應封包內的標頭內容和狀態碼，跟前兩者比較起來，該方法可以寫除了location以外的標頭設定

### 回應封包內的location 標頭
[[@mdnLocationHTTPMDN]] 所描述：
> The **`Location`** response header indicates the URL to redirect a page to. It only provides a meaning when served with a `3xx` (redirection) or `201` (created) status response.

重點：
- location是主要是伺服器要求客戶端導向指定路由的標頭
- 通常會搭配3xx

## 複習
#🧠 回應封包內的location 標頭 是做什麼？會搭配狀態碼嗎 ->->-> `location是主要是伺服器要求客戶端導向指定路由的標頭，通常會搭配`

#🧠  在express server中，res.location是做什麼用的 ->->-> `直接設定回應封包內的location標頭`

#🧠 在express server中，res.redirect是做什麼用的 ->->-> `res.redirect 是直接設定回應封包內的location標頭和狀態碼`

#🧠 在express server中，伺服器執行res.redirect會直接使客戶端導向嗎 ->->-> `並不會，只是先撰寫回應封包內的location標頭和狀態碼`

#🧠 在express server中，res.writeHead是做什麼用的 ->->-> `是直接設定回應封包內的標頭內容和狀態碼`
#🧠 在express server中，res.writeHead 與res.location、res.redirect之間差別會是什麼 ->->-> `跟前兩者比較起來，該方法可以寫除了location以外的標頭設定`
<!--SR:!2022-07-07,3,250-->

---
Status: #🧠 
Tags:
[[Express]]
Links:
References:
[[@node.jsHTTPNodeJs]]
[[@mdnLocationHTTPMDN]]
[[@expressExpressAPICanZhao]]