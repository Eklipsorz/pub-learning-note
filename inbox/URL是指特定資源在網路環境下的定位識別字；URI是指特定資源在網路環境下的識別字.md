## 描述

> 統一資源標識符（英語：Uniform Resource Identifier，縮寫：URI）在電腦術語中是用於標識某一網際網路資源名稱的字串

> 通用URI的格式如下：

> \[協定名\]:\/\/\[使用者名稱\]:\[密碼\]\@\[主機名\]\:\[埠\]\/\[路徑\]\?\[查詢參數\]\#\[片段ID\]


[[@danielmiesslerDifferenceURLURI]]
> 1.  A UR**I** is an **identifier** of a specific resource. Examples: _Books, Documents_
> 2.  A UR**L** is special type of identifier **that also tells you how to access it**. Examples: _HTTP, FTP, MAILTO_
>3.  If the protocol (`https`, `ftp`, etc.) is either present or implied for a domain, **you should call it a URL**—even though it’s also a URI.

> -   A Uniform Resource Identifier (`URI`) is a string of characters that uniquely identify a name or a resource on the internet. A `URI` _identifies a resource by name, location, or both_. URIs have two specializations known as Uniform Resource Locator (URL), and Uniform Resource Name (`URN`). 
> -   A Uniform Resource Locator (`URL`) is a type of URI that specifies not only a resource, _but how to reach it on the internet—like `http://`, `ftp://`, or `mailto://`_.
> -   A Uniform Resource Name (`URN`) is a type of URI _that uses the specific naming scheme of `urn:`_—like `urn:isbn:0-486-27557-4` or `urn:isbn:0-395-36341-1`.
    -   So a `URI` or `URN` is like your name, and a `URL` is a specific subtype of `URI` that’s like your name combined with your address.

[[@wikidataTongYiZiYuanDingWeiFuWeiJiBaiKeZiYouDeBaiKeQuanShu]]
> 以「https://zh.wikipedia.org:443/w/index.php?title=隨機頁面」爲例，其中：

> 1.  **https**，是協定；
>2.  **zh.wikipedia.org**，是伺服器；
>3.  **443**，是伺服器上的網路埠號；
>4.  **/w/index.php**，是路徑；
>5.  **?title=Special:隨機頁面**，是詢問。

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665912842/blog/REST/URI-Example_wruozs.png)

重點：
- URL (Uniform Resource Locator) 是指特定資源在網路環境下的定位識別字，其識別字會是由schema、host、port、path 所構成
- URI (Uniform Resource Identifier) 是指特定資源在網路環境下的識別字，其識別字會是由schema、host、port、path、query string、#fragment 所構成
- path 本身是指資源所在的絕對路徑，該路徑會以伺服器本身網路位置來定位，由目錄和檔案所構成

## 複習


#🧠 URL 完整名稱為->->-> `Uniform Resource Locator`
<!--SR:!2022-11-26,28,250-->

#🧠 URI 完整名稱為 ->->-> `Uniform Resource Identifier`
<!--SR:!2022-11-07,13,230-->

#🧠 URL (Uniform Resource Locator) 是什麼？由什麼構成？->->-> `特定資源在網路環境下的定位識別字，其識別字會是由schema、host、port、path 所構成`
<!--SR:!2022-11-17,21,250-->

#🧠 URI (Uniform Resource Identifier) 是什麼？由什麼構成 ->->-> `特定資源在網路環境下的識別字，其識別字會是由schema、host、port、path、query string、#fragment`
<!--SR:!2022-11-10,17,248-->

#🧠 URL & URI 的 path 是什麼？ ->->-> `本身是指資源所在的絕對路徑，該路徑會以伺服器本身網路位置來定位`
<!--SR:!2022-11-09,16,248-->

#🧠 URL & URI ：path 本身是指資源所在的絕對路徑，該路徑會以伺服器本身網路位置來定位，以檔案系統來說，由什麼構成->->-> `由目錄和檔案所構成`
<!--SR:!2022-11-09,16,248-->


#🧠 https:\/\/zh.wikipedia.org:443\/w\/index.php?title=隨機頁面 為例，哪一段是URL？哪一段才是URI ->->-> `https://zh.wikipedia.org:443/w/index.php為URL，而https://zh.wikipedia.org:443/w/index.php?title=隨機頁面為URI`
<!--SR:!2022-11-10,17,248-->





---
Status: #🌱 
Tags:
Links:
References:
[[@danielmiesslerDifferenceURLURI]]
[[@wikidataTongYiZiYuanDingWeiFuWeiJiBaiKeZiYouDeBaiKeQuanShu]]