

## 描述
QueryString 加號問題 - 伺服器在解析query參數時就會自動以無UTF8形式來解碼，其+被解出來會是空白


### 詳細問題描述


[[@heartfootprintXueXiBeiWangLuQueryStringShiJiaHaoBianKongBaiDeWenTi]] 和
https://www.cnblogs.com/CrazyCoder/archive/2007/10/17/928261.html
> 现在手上的项目中使用了ClickOnce技术来部署客户端，客户端有时需要从服务器传一些参数，对于ClickOnce部署的程序来说我们可以在launch的URL中使用query strings来达到这一目的。参照MSDN上的文章，很快就写完了代码。好了，试试看。部署，从服务器launch客户端，似乎一切正常，所有参数的值都顺利得到了。

> 可还没等Check-in代码，一个测试就失败了。Debug了半天才发现原来是一个参数值中又加号：+。在使用HttpUtility.ParseQueryString分析query string后参数值中的加号变成了空格，以前似乎没遇到过这样的现象。[Google](http://www.google.cn/search?q=querystring+plus+sign&complete=1&hl=zh-CN&newwindow=1&rlz=1T4GGIG_enCN241CN241)了一下才知道原来加号在query string是保留用来代表空格的，要在query string中传这些保留字符必须对query string进行编码。

> 修改了服务端的代码，想当然的在客户端加了decode的方法，没想到结果还是不对。查了MSDN关于HttpUtility.ParseQueryString方法的帮助才知道原来这个方法内置会对query string进行解码（decode）并返回包含结果的NameValueCollection。

> 忙了半天最后终于搞定了。

> 总结一下：

> 1）安全起见query string一定要encode
> 2）HttpUtility.ParseQueryString会自动做decode，不要画蛇添足。


### +
[[@albionresearchltdURLEncodeURLDecodePage]]所描述：
> This web page encodes or decodes a string using URL Encoding. URL Encoding is used when placing text in a query string to avoid it being confused with the URL itself. It is normally used when the browser sends form data to a web server.

[[@domlaoSignQueryString2011]]和[[@palAnswerSignQuery2011]] 所描述：

> `+` sign has a semantic meaning in the query string. It is used to represent a space. Another character that has semantic importance in the query string is `&` which is used to separate the various `var=value` pairs in the query string.

> Most server side scripts would decode the query parameters before using them, so that a `+`gets properly converted to a space. Now, if you want a literal `+` to be present in the query string, you need to specify `%2B` instead.

> `+` sign in the query string is URL-decoded to a space. `%2B` in the query string is URL-decoded to a + sign.



[[@wikidataBaiFenHaoBianMaWeiJiBaiKeZiYouDeBaiKeQuanShu]] 所描述：
> 當HTML表單中的資料被提交時，表單的域名與值被編碼並通過HTTP的GET或者POST方法甚至更古遠的email[2]把請求傳送給伺服器。這裡的編碼方法採用了一個非常早期的通用的URI百分號編碼方法，並且有很多小的修改如換行規格化以及把空格符的編碼"%20"替換為"+" 。按這套方法編碼的資料的MIME類型是application/x-www-form-urlencoded，當前仍用於（雖然非常過時了）HTML與XForms規範中。此外，CGI規範包括了web伺服器如何解碼這類資料、利用這類資料的內容。

> 如果傳送的是HTTP GET請求，application/x-www-form-urlencoded資料包含在所請求URI的查詢成分中。如果傳送的是HTTP POST請求或通過email，資料被放置在訊息體中，媒體類型的名字被包含在訊息的Content-Type頭內部。




重點：
- querystring 和 網址一率皆以URL編碼算法或者百分比算法來進行解法和編碼
- 其URL編碼算法或者百分比算法會考慮UTF編碼系統而加以擴充自己編碼庫，但早期的URL編碼算法沒考慮UTF編碼系統而擴充，導致只有UTF-8編碼能辨識的字元無法在URL編碼和解碼上獲得正確的值，比如：
	- 早期URL編碼系統：
		- 可以正常編碼/解析不加百分比為主的字元，比如A-Z
		- 可以正常編碼/解析加百分比為主的字元
		- 編碼系統存在具有特殊用途的特殊字元，如+號，系統讀取到會直接解碼成空白
	- 若要避免的話，可先將編碼內容上+轉換成純粹的百分比編碼
	- 較新URL編碼系統：會將以容忍UTF編碼將(編碼過後的字元)+視為URL編碼系統的合法字元，不會在解碼的時候，又以原本百分比編碼的規則解碼成空白
- 客戶端傳遞URL Query參數至伺服器時，伺服器總是會先以百分比編碼來解碼



### 案例


編碼方：
```
daeaf+wadadwa+dasddaw
```


解碼方：
```
daeaf wadadwa dasddaw
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656580534/blog/encode-and-decode/querystring-decoded-text_djvibd.png)

[[@albionresearchltdURLEncodeURLDecodePage]] 所描述：
> RFC2396 mode (no Unicode or UTF8, space encoded as ‘+’)

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References:
[[@heartfootprintXueXiBeiWangLuQueryStringShiJiaHaoBianKongBaiDeWenTi]]
[[@domlaoSignQueryString2011]]
[[@palAnswerSignQuery2011]]
[[@albionresearchltdURLEncodeURLDecodePage]]
[[@wikidataBaiFenHaoBianMaWeiJiBaiKeZiYouDeBaiKeQuanShu]]