

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


重點：
- 客戶端傳遞以百分比編碼為主的Query string 至伺服器，伺服器收到會立即以百分比編碼解碼，內容會是沒添加百分比的形式和參雜+，其中會將+視為空白，這是由於伺服器解碼是比較早期的百分比編碼系統
- 解法是：替整個Query string以百分比編碼重新編碼

### Query String
[[@wikidataQueryString2022]] 所描述
> A **query string** is a part of a uniform resource locator (URL) that assigns values to specified parameters

> Typical URL containing a query string is as follows:

> `https://example.com/over/there?name=ferret`

> When a server receives a request for such a page, it may run a program, passing the query string, which in this case is `name=ferret`, unchanged to the program. The question mark is used as a separator, and is not part of the query string

重點：
- query string 是用來向特定伺服器索要特定資源的請求字串，以URL形式來表示，比如：
`https://example.com/over/there?name=ferret`
- query string 在客戶端和伺服器之間會以百分比編碼或者URL編碼

### 百分比編碼/URL編碼
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
- querystring 和 網址一率皆以URL編碼算法或者百分比算法來進行解碼和編碼
- 其URL編碼算法或者百分比算法會考慮UTF編碼系統而加以擴充自己編碼庫，但早期的URL編碼算法沒考慮UTF編碼系統而擴充，導致只有UTF-8編碼能辨識的字元無法在URL編碼和解碼上獲得正確的值，比如：
	- 早期(包含現在)URL編碼系統一編碼後的內容：
		- 會是以百分比為主的字元：不是單純0-9、A-Z、a-z的字元，除了英文以外，還有如各國的語言文字
		- 不加百分比為主的字元，比如A-Z
		- 編碼系統存在具有特殊用途的特殊字元，如+號
	- 以下內容面對早期URL編碼系統的解碼會是：
		- 不加百分比為主的字元，比如A-Z ->(經過解碼) 不加百分比為主的字元，比如A-Z
		- 加百分比為主的字元 -> (經過解碼) 百分比編碼前的字元
		- 編碼系統存在具有特殊用途的特殊字元，如+號 -> (經過解碼) 會轉換其他字元，如+號就是空白 
		- 若要避免的話，可先將編碼內容上+轉換成純粹的百分比編碼
	- 較新URL編碼系統：會將以容忍UTF編碼為主來解碼，在這裡由於+是在UTF編碼裡頭，所以在解碼的時候，會變成+，而非空白
- 客戶端傳遞URL Query參數至伺服器時，伺服器總是會先以百分比編碼來解碼



### 案例
若假設客戶端傳遞一份以百分比編碼過來的字串，
編碼方：
```
daeaf+wadadwa+dasddaw
```


伺服器收到後，會直接解碼：除了+由於是百分比編碼系統的特殊字元而被轉換成空白以外，剩下會正常解析
```
daeaf wadadwa dasddaw
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656580534/blog/encode-and-decode/querystring-decoded-text_djvibd.png)

[[@albionresearchltdURLEncodeURLDecodePage]] 所描述：
> RFC2396 mode (no Unicode or UTF8, space encoded as ‘+’)

## 複習
#🧠  querystring 和 網址一率在客戶端和伺服器之間的傳遞間會以什麼編碼形式進行？請舉例誰編碼誰解碼 ->->-> `會以百分比編碼來進行編碼和解碼，當客戶端傳遞百分比編碼形式的編碼字元至伺服器，伺服器收到就會立即以百分比編碼來解碼`

#🧠 百分比編碼編碼後的形式會是什麼 ->->-> `以百分比符號和對應特定數值為主、	- 會是以百分比為主的字元 - 不加百分比為主的字元，比如A-Z - 編碼系統存在具有特殊用途的特殊字元，如+號`

#🧠 百分比編碼編碼後的形式結果會是 會是以百分比為主的字元，被轉換前的字元通常會是什麼->->-> `不是單純0-9、A-Z、a-z的字元，除了英文以外，還有如各國的語言文字`


#🧠 假如以不考慮UTF編碼的百分比編碼能夠接受的解碼形式會是如何？換言之，若輸入不為百分比編碼的話，會怎麼樣解碼 ->->-> `- 可以正常編碼/解析不加百分比為主的字元，比如A-Z - 可以正常編碼/解析加百分比為主的字元 - 編碼系統存在具有特殊用途的特殊字元，如+號，系統讀取到會直接解碼成空白`

#🧠 假如以考慮UTF編碼的百分比編碼能夠接受的解碼形式會是如何？換言之，若輸入不為百分比編碼的話，會怎麼樣解碼   ->->-> ``- 可以正常編碼/解析不加百分比為主的字元，比如A-Z，- 可以正常編碼/解析加百分比為主的字元 - 編碼系統存在具有特殊用途的特殊字元，系統讀取到會直接解碼成空白 - 一些能夠在UTF編碼解析且會被早期百分比編碼當作是特殊字元的字元。`

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會如何處理？會先解析嗎？又會解析成什麼內容？ (以不考慮UTF8編碼的百分比編碼來說)->->-> `伺服器會先解析，在這裡由於是不考慮UTF8編碼的百分比編碼來解碼，所以除了+由於是百分比編碼系統的特殊字元而被轉換成空白以外，剩下會正常解析，結果會是daeaf wadadwa dasddaw

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會如何處理？會先解析嗎？又會解析成什麼內容？ (以考慮UTF8編碼的百分比編碼來說)->->-> `會先解析，並且解析成daeaf+wadadwa+dasddaw，在這裡+的確會是早期百分比編碼系統的特殊字元，但考慮UTF8編碼的百分比編碼會將+視為一般字元`

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會以百分比編碼解碼成daeaf+wadadwa+dasddaw？為什麼不會將+視為空白？->->-> `在這裡+的確會是早期百分比編碼系統的特殊字元，但考慮UTF編碼的百分比編碼會將+視為一般字元，而支援UTF編碼的百分比編碼會由於這點會把+視為一般字元，而非空白`

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，而伺服器會先解析並解析成daeaf wadadwa dasddaw，那如果不想被誤解成空白，那麼該如何解決？->->-> `將daeaf+wadadwa+dasddaw以百分比編碼正式編碼成擁有百分比符號的字元。`


---
Status: #🌱 
Tags:
[[Service]]
Links:
References:
[[@wikidataQueryString2022]]
[[@heartfootprintXueXiBeiWangLuQueryStringShiJiaHaoBianKongBaiDeWenTi]]
[[@domlaoSignQueryString2011]]
[[@palAnswerSignQuery2011]]
[[@albionresearchltdURLEncodeURLDecodePage]]
[[@wikidataBaiFenHaoBianMaWeiJiBaiKeZiYouDeBaiKeQuanShu]]