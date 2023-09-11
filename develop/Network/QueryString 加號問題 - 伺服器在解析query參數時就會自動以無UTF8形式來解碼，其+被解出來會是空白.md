

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
~~[[@wikidataQueryString2022]] 所描述
> A **query string** is a part of a uniform resource locator (URL) that assigns values to specified parameters~~

> ~~Typical URL containing a query string is as follows:~~

> ~~`https://example.com/over/there?name=ferret`~~

> ~~When a server receives a request for such a page, it may run a program, passing the query string, which in this case is `name=ferret`, unchanged to the program. The question mark is used as a separator, and is not part of the query string~~

~~重點：~~
- ~~query string 是用來向特定伺服器索要特定資源的請求字串，以URL形式來表示，比如：
`https://example.com/over/there?name=ferret`~~
- ~~query string 在客戶端和伺服器之間會以百分比編碼或者URL編碼~~

[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]

### 百分比編碼/URL編碼
[[@albionresearchltdURLEncodeURLDecodePage]]所描述：
> This web page encodes or decodes a string using URL Encoding. URL Encoding is used when placing text in a query string to avoid it being confused with the URL itself. It is normally used when the browser sends form data to a web server.

[[@domlaoSignQueryString2011]]和[[@palAnswerSignQuery2011]] 所描述：

> `+` sign has a semantic meaning in the query string. It is used to represent a space. Another character that has semantic importance in the query string is `&` which is used to separate the various `var=value` pairs in the query string.

> Most server side scripts would decode the query parameters before using them, so that a `+`gets properly converted to a space. Now, if you want a literal `+` to be present in the query string, you need to specify `%2B` instead.

> `+` sign in the query string is URL-decoded to a space. `%2B` in the query string is URL-decoded to a + sign.


> 2005年1月發布的RFC 3986，建議所有新的URI必須對未保留字元不加以百分號編碼；其它字元建議先轉換為UTF-8位元組序列, 然後對其位元組值使用百分號編碼

[[@wikidataBaiFenHaoBianMaWeiJiBaiKeZiYouDeBaiKeQuanShu]] 所描述：
> 當HTML表單中的資料被提交時，表單的域名與值被編碼並通過HTTP的GET或者POST方法甚至更古遠的email[2]把請求傳送給伺服器。這裡的編碼方法採用了一個非常早期的通用的URI百分號編碼方法，並且有很多小的修改如換行規格化以及把空格符的編碼"%20"替換為"+" 。按這套方法編碼的資料的MIME類型是application/x-www-form-urlencoded，當前仍用於（雖然非常過時了）HTML與XForms規範中。此外，CGI規範包括了web伺服器如何解碼這類資料、利用這類資料的內容。

> 如果傳送的是HTTP GET請求，application/x-www-form-urlencoded資料包含在所請求URI的查詢成分中。如果傳送的是HTTP POST請求或通過email，資料被放置在訊息體中，媒體類型的名字被包含在訊息的Content-Type頭內部。

#### querystring 和 網址的編碼
querystring 和 網址一率皆以URL編碼算法或者百分比算法來進行解碼和編碼

#### 只支援ASCII編碼的URL編碼
URL編碼系統將編碼前的字元分為兩種：
	- 未保留字元：URL編碼認定沒特定用途的字元，編碼並不會編碼；解碼並不會解析，只會跟編碼前一樣
	> Characters from the unreserved set never need to be percent-encoded.
	- 保留字元：URL編碼認定具有特殊用途的字元，解碼時會按照用途解析成特定內容
	> When a character from the reserved set (a "reserved character") has a special meaning (a "reserved purpose") in a certain context
	
URL編碼系統的編碼遇到以下內容：
 - 保留字元要轉換成未保留字元：則需要從保留字元轉換成以百分比為主的字元符號
 - 未保留字元：被編碼的形式還是會跟編碼前一樣
 - 保留字元：被編碼的形式還是會跟編碼前一樣

URL 編碼系統的解碼遇到以下內容：
- 百分比為主的字元符號：從百分比為主的字元符號轉換成被編碼前的樣子
- 未保留字元：被解碼的形式還是會跟編碼前一樣
- 保留字元：被解碼的形式會按照其字元在編碼系統所擁有的用途來解析


#### 支援ASCII編碼和UTF編碼的URL編碼
> 2005年1月發布的RFC 3986，建議所有新的URI必須對未保留字元不加以百分號編碼；其它字元建議先轉換為UTF-8位元組序列, 然後對其位元組值使用百分號編碼


URL編碼系統將編碼前的字元分為4種：
	- 未保留字元：URL編碼認定沒特定用途的字元，編碼並不會編碼；解碼並不會解析，只會跟編碼前一樣
	> Characters from the unreserved set never need to be percent-encoded.
	- 保留字元：URL編碼認定具有特殊用途的字元，解碼時會按照用途解析成特定內容
	> When a character from the reserved set (a "reserved character") has a special meaning (a "reserved purpose") in a certain context
	- UTF編碼字元
	- 部分保留字元直接被當作未保留字元看待，如+號
	
	
URL編碼系統的編碼遇到以下內容：
 - 保留字元要轉換成未保留字元：則是要看是否新版編碼系統是否有把當前保留字元視為未保留字元，若有的話，就依照未保留字元來處理，若沒有就從保留字元轉換成以百分比號為主的編碼形式
 - 未保留字元：被編碼的形式還是會跟編碼前一樣
 - 保留字元：則是要看是否新版編碼系統是否有把當前保留字元視為未保留字元，若有的話，就依照未保留字元來處理，若沒有就依照保留字元來處理
 - UTF編碼字元：UTF編碼形式的字元會先轉換成UTF-8編碼，然後再針對實際編碼值來以百分比編碼轉換

URL 編碼系統的解碼遇到以下內容：
- 百分比為主的字元符號：從百分比為主的字元符號轉換成被編碼前的樣子
- 未保留字元：被解碼的形式還是會跟編碼前一樣
- 保留字元：則是要看是否新版編碼系統是否有把當前保留字元視為未保留字元，若有的話，就依照未保留字元來處理，若沒有就依照保留字元來處理


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
<!--SR:!2025-01-11,552,250-->

#🧠 早期只支援ASCII編碼的URL編碼會將編碼前的字元分為哪兩種 ->->-> `	- 未保留字元：URL編碼認定沒特定用途的字元，編碼並不會編碼；解碼並不會解析，只會跟編碼前一樣 - 保留字元：URL編碼認定具有特殊用途的字元，解碼時會按照用途解析成特定內容`
<!--SR:!2024-04-09,392,250-->

#🧠 只支援ASCII編碼的URL編碼遇到的字元是保留字元的話，其編碼形式會是如何？ ->->-> `被編碼的形式還是會跟編碼前一樣`
<!--SR:!2024-03-28,356,230-->

#🧠 只支援ASCII編碼的URL編碼遇到的字元是未保留字元的話，其編碼形式會是如何？ ->->-> `被編碼的形式還是會跟編碼前一樣`
<!--SR:!2023-12-04,313,250-->

#🧠 只支援ASCII編碼的URL編碼遇到的字元是保留字元的話，但想把該保留字元轉換成未保留字元來編碼，其編碼形式會是如何？ ->->-> `則需要從保留字元轉換成以百分比為主的字元符號`
<!--SR:!2023-11-26,308,250-->


#🧠 只支援ASCII編碼的百分比編碼編碼後的形式結果會是 會是以百分比為主的字元，被轉換前的字元通常會是什麼->->-> `原本會被百分比編碼解碼成特殊用途且想以一般字元來顯示的字元`
<!--SR:!2024-06-10,435,250-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼編碼後的形式結果會是 會是以百分比為主的字元，被轉換前的字元通常會是什麼 ->->-> `UTF編碼、URL編碼系統的保留字元`
<!--SR:!2024-05-13,410,250-->


#🧠 假如以 只支援ASCII編碼的URL編碼會有的解碼形式是什麼？ ->->-> `		-   百分比為主的字元符號：從百分比為主的字元符號轉換成被編碼前的樣子 -   未保留字元：被解碼的形式還是會跟編碼前一樣 -   保留字元：被解碼的形式會按照其字元在編碼系統所擁有的用途來解析 `
<!--SR:!2024-09-09,487,250-->


#🧠 假如以支援ASCII編碼和UTF編碼的百分比編碼會有的解碼形式是什麼 ->->-> `-   百分比為主的字元符號：從百分比為主的字元符號轉換成被編碼前的樣子 -   未保留字元：被解碼的形式還是會跟編碼前一樣 -   保留字元：被解碼的形式會按照其字元在編碼系統所擁有的用途來解析`
<!--SR:!2023-12-30,109,190-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼會將字元分為哪4種？->->-> `未保留字元：URL編碼認定沒特定用途的字元，編碼並不會編碼；解碼並不會解析，只會跟編碼前一樣、保留字元：URL編碼認定具有特殊用途的字元，解碼時會按照用途解析成特定內容、 UTF編碼字元、部分保留字元直接被當作未保留字元看待，如+號`
<!--SR:!2024-04-25,404,250-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼，若想將未保留字元做編碼，其編碼流程和形式會是如何  ->->-> `被編碼的形式還是會跟編碼前一樣`
<!--SR:!2024-01-10,335,250-->

#🧠  支援ASCII編碼和UTF編碼的URL編碼，若針對UTF編碼字元來編碼，其流程和形式會是如何->->-> `會先將該字元轉換成UTF編碼值，然後針對編碼值依照百分比編碼來重新編碼，最後會是以百分比形式`
<!--SR:!2024-01-09,334,250-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼，若針對想從保留字元要轉換成未保留字元的保留字元，其編碼流程和形式會是如何 ->->-> `-   保留字元要轉換成未保留字元：則是要看是否新版編碼系統是否有把當前保留字元視為未保留字元，若有的話，就依照未保留字元來處理，若沒有就從保留字元轉換成以百分比號為主的編碼形式`
<!--SR:!2024-04-26,403,250-->

#🧠  支援ASCII編碼和UTF編碼的URL編碼，其保留字元的解碼是？->->-> `則是要看是否新版編碼系統是否有把當前保留字元視為未保留字元，若有的話，就依照未保留字元來處理，若沒有就依照保留字元來處理`
<!--SR:!2023-09-14,2,248-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼，其百分比為主的字元符號的解碼是？ ->->-> `從百分比為主的字元符號轉換成被編碼前的樣子`
<!--SR:!2023-11-15,301,250-->

#🧠 支援ASCII編碼和UTF編碼的URL編碼，未保留字元的解碼是？ ->->-> `被解碼的形式還是會跟編碼前一樣`
<!--SR:!2023-10-23,289,250-->

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會如何處理？會先解析嗎？又會解析成什麼內容？ (以支援ASCII編碼的URL編碼)->->-> `伺服器會先解析，在這裡由於是支援ASCII編碼的URL編碼，會將+視為空白的字元`
<!--SR:!2024-09-13,491,250-->

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會如何處理？會先解析嗎？又會解析成什麼內容？ (以支援ASCII編碼和UTF編碼的URL編碼)->->-> `會先解析，並且解析成daeaf+wadadwa+dasddaw，在這裡+的確會是早期百分比編碼系統的特殊字元，但考慮UTF8編碼的百分比編碼會將+視為一般字元`
<!--SR:!2024-09-01,484,250-->

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，伺服器會以百分比編碼解碼成daeaf+wadadwa+dasddaw？為什麼不會將+視為空白？->->-> `代表著伺服器的編解碼系統是採用較新版本的URL編碼，而較新版本的URL編碼會將+這個特殊字元，視為非保留字元來看待`
<!--SR:!2025-01-13,554,250-->

#🧠 假如我們將字元daeaf+wadadwa+dasddaw傳遞至伺服器，而伺服器會先解析並解析成daeaf wadadwa dasddaw，那如果不想被誤解成空白，那麼該如何解決？->->-> `將daeaf+wadadwa+dasddaw以百分比編碼正式編碼成擁有百分比符號的字元。`
<!--SR:!2024-07-16,454,250-->


---
Status: #🌱 
Tags:
[[Service]]
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
References:
[[@wikidataQueryString2022]]
[[@heartfootprintXueXiBeiWangLuQueryStringShiJiaHaoBianKongBaiDeWenTi]]
[[@domlaoSignQueryString2011]]
[[@palAnswerSignQuery2011]]
[[@albionresearchltdURLEncodeURLDecodePage]]
[[@wikidataBaiFenHaoBianMaWeiJiBaiKeZiYouDeBaiKeQuanShu]]