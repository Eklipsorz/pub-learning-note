## 描述


[[@rcreativeUnderscoreAllowedURL]]
> Is it allowed, yes it’s allowed.

> Is it recommended? No it’s not recommended to use underscore in an URL.

> Underscore would lead to Complex URLs, it can cause a problems for crawlers by creating unnecessarily high numbers of URLs that point to identical or similar content on your site. As a result, some crawler may consume much more bandwidth than necessary, or may be unable to completely index all the content on your site.



[[@WangZhiUrlsYingGaiYongDuanHengXian]]
> Matt Cutts 曾經說過，Google 在看待短橫線（-）跟下底線時，採用不同的處理方式，短橫線（-）直接被當成分隔來處理，也就是空格斷點。

> 例如網址中如果有 “black-cat”其實就會被解讀成「black cat」。

> 但是如果你的網址裡面的英文是「black_cat」，那麼其實 Google 在解析的時候，就會解讀成完整的「black_cat」，也就是 Google 並不會將下底線（_）當成空格處理

> 雖然 Matt Cutts 後面有提到，其實這並不是一個影響性很大的要素，但是在 SEO 搜尋引擎優化的實務作法上，還是會建議要使用短橫線（dash）而不是底線（Underscore）。


重點：
- 理論上當端點會是 A-B 和 A_B時，瀏覽器、ㄙ會正常解讀
- 在Google SEO 爬蟲
A-B=> 連字號會被都成是separator，會分隔成A和B這兩個字串來進行index，比如

Red-widget 就會是 red 和 widget 

  

A_B => 下底線不會被當成separator，而是當成A_B這整串字串，不會分隔成A和B這兩個字串


## 複習


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@rcreativeUnderscoreAllowedURL]]
[[@WangZhiUrlsYingGaiYongDuanHengXian]]