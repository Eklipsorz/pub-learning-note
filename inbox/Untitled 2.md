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
	- 主要面向於客戶端的請求處理，主要會是要求客戶端直接導向目標URL 所指向的頁面
	- 會將瀏覽器上所顯示的URL更改成目標URL
- rewrite：
	- 主要面向於伺服器的請求處理，主要會在伺服器接收到封包時，在正式處理前會將封包指示的端點改寫成指定端點，然後在正式處理就以改寫後的端點來處理
	- 不會將瀏覽器所顯示的URL更改成目標URL，因為這是發生伺服器內部上的轉換
- 案例：redirect：
	- 



## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References:
[[@scottforsythURLRewriteVs]]