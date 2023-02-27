## 描述

[[@scottforsythURLRewriteVs]]
> Simply put, a redirect is a **client-side** request to have the web browser go to another URL. This means that the URL that you see in the browser will update to the new URL.

> A rewrite is a **server-side** rewrite of the URL before it’s fully processed by IIS. This will not change what you see in the browser because the changes are hidden from the user.


> redirect 
> - Client-side
> - Changes URL in browser address bar

> rewrite
> - Server-side
> - Doesn’t change URL in browser address bar


Redirect Example：
```
http://yourdomain.com to http://www.yourdomain.com in the browser
```

Rewrite Example：
```
http://localtest.me/articles/how-to-win-at-chess is a friendly URL for http://localtest.me/articles.aspx?name=now-to-win-at-chess
```


重點：
- redirect ：
	- 面向於客戶端的請求處理，主要會是要求客戶端直接導向目標URL 所指向的頁面來發送請求
	- 會將瀏覽器上所顯示的URL更改成目標URL
- rewrite：
	- 面向於伺服器的請求處理，主要會在伺服器接收到封包時，在正式處理前會將封包指示的端點改寫成指定端點，然後在正式處理就以改寫後的端點來處理
	- 不會將瀏覽器所顯示的URL更改成目標URL，因為這是發生在伺服器內部上的轉換
- 案例：redirect
	- 當瀏覽器對yourdomain.com對應伺服器以/發送請求，瀏覽器就直接被導向至www.yourdomain.com
  ```
   http://yourdomain.com to http://www.yourdomain.com in the browser
  ```
- 案例：rewrite
	- 當瀏覽器對localtest.me對應伺服器以articles/how-to-win-at-chess端點發送請求，伺服器接收到並於正式處理前就直接更改成articles.aspx?name=now-to-win-at-chess，然後伺服器就以改寫後結果來處理。
  ```
  http://localtest.me/articles/how-to-win-at-chess is a friendly URL for 
  http://localtest.me/articles.aspx?name=now-to-win-at-chess
  ```

### 簡單比較：redirect vs. rewrite

1. 前者是client side的請求處理，後者是server side的請求處理
2. 前者是直接將瀏覽器導向目標URL，後者則是將瀏覽器指定的URL在伺服器內做URL轉換
3. 前者是會更改瀏覽器顯示的URL，後者則不會


## 複習

#🧠 redirect 是面向於什麼的處理？ ->->-> `面向於客戶端的請求處理`
<!--SR:!2023-07-30,194,250-->

#🧠 redirect 用途是做了什麼？ ->->-> `主要會是要求客戶端直接導向目標URL 所指向的頁面來發送請求`
<!--SR:!2023-05-30,94,230-->


#🧠 redirect 用途是直接導向目標URL 所指向的頁面來發送請求，那具體還會修改什麼跟URL相關的？ ->->-> `會將瀏覽器上所顯示的URL更改成目標URL`
<!--SR:!2023-02-27,41,230-->

#🧠 rewrite 是面向於什麼的處理->->-> `面向於伺服器的請求處理`
<!--SR:!2023-07-30,194,250-->


#🧠 rewrite 用途是做了什麼？ ->->-> `主要會在伺服器接收到封包時，在正式處理前會將封包指示的端點改寫成指定端點，然後在正式處理就以改寫後的端點來處理`
<!--SR:!2023-07-21,185,250-->

#🧠 rewrite 用途是主要會在伺服器接收到封包時，在正式處理前會將封包指示的端點改寫成指定端點，然後在正式處理就以改寫後的端點來處理，會直接修改瀏覽器的顯示URL嗎？為什麼？ ->->-> `不會，具體因爲這是發生在伺服器內部上的轉換`
<!--SR:!2023-07-25,189,250-->

#🧠 簡單比較：redirect vs. rewrite? ->->-> `1. 前者是client side的請求處理，後者是server side的請求處理 2. 前者是直接將瀏覽器導向目標URL，後者則是將瀏覽器指定的URL在伺服器內做URL轉換 3. 前者是會更改瀏覽器顯示的URL，後者則不會`
<!--SR:!2023-05-31,93,230-->


#🧠 請用以下例子來說明redirect： yourdomain.com to www.yourdomain.com ->->-> `當瀏覽器對yourdomain.com對應伺服器以/發送請求，瀏覽器就直接被導向至www.yourdomain.com`
<!--SR:!2023-07-23,187,250-->

#🧠  請用以下例子來說明rewrite：localtest.me/articles/how-to-win-at-chess to localtest.me/articles.aspx?name=now-to-win-at-chess ->->-> `當瀏覽器對localtest.me對應伺服器以articles/how-to-win-at-chess端點發送請求，伺服器接收到並於正式處理前就直接更改成articles.aspx?name=now-to-win-at-chess，然後伺服器就以改寫後結果來處理。`
<!--SR:!2023-07-30,194,250-->

#🧠 rewrite vs. redirect 誰會更改瀏覽器所顯示URL->->-> `redirect`
<!--SR:!2023-07-30,194,250-->


---
Status: #🌱 
Tags:
Links:
References:
[[@scottforsythURLRewriteVs]]