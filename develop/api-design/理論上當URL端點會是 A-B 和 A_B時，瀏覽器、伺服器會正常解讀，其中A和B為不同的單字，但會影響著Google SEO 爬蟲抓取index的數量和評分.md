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
- 理論上當端點會是 A-B 和 A_B時，瀏覽器、伺服器會正常解讀，其中A和B為不同的單字
- 但在Google SEO 爬蟲來看，會將A-B和A_B進行特定處理，其結果會用來以index來綁定該對應網頁並作為關聯評分上：
	- A-B： 連字號**-**會被都成是separator，會分隔成A和B這兩個字串來進行index，比如Red-widget 就會是 red 和 widget 
	- A_B ： 下底線不會被當成separator，而是當成A_B這整串字串，不會分隔成A和B這兩個字串
- 若選用A-B，會以A、B、A B這兩單字作為index和關鍵字評分上，會讓使用者多了更多字串來找到對應網站以及使關鍵字搜尋排名更高
- 若選用A_B，只是單方對以A_B這單字作為index和評分上，相較於上者，使用者更難以找得到網站

## 複習

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，那麼伺服器、瀏覽器能正常解讀他們嗎 ->->-> `都能正常解讀`
<!--SR:!2025-02-08,505,250-->

#🧠 理論上當URL端點會是red-widget 或者 red_widget，那麼伺服器、瀏覽器哪個不能解讀？->->-> `都能解讀`
<!--SR:!2024-12-30,475,250-->

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，那麼伺服器、瀏覽器能正常解讀他們，那麼真正使人建議選用A-B的原因會是什麼？ ->->-> `在於Google SEO 爬蟲是否能替對應網站建立更多index和提高SEO`
<!--SR:!2024-10-14,426,250-->

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，在Google 爬蟲來看的話，會如何解析他們來作為index？ ->->-> `A-B： 連字號**-**會被都成是separator，會分隔成A和B這兩個字串來進行index；A_B ： 下底線不會被當成separator，而是當成A_B這整串字串，不會分隔成A和B這兩個字串`
<!--SR:!2024-01-03,222,230-->

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，在Google 爬蟲來看的話，會分別建立哪些index來評分 ->->-> `A-B：A、B、A B； A_B：A_B`
<!--SR:!2023-12-30,99,230-->

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，在Google 爬蟲來看的話，若選用A-B的好處會是什麼 ->->-> `若選用A-B，會以A、B、A B這兩單字作為index和關鍵字評分上，會讓使用者多了更多字串來找到對應網站以及使關鍵字搜尋排名更高`
<!--SR:!2024-10-18,430,250-->

#🧠 理論上當URL端點會是 A-B 或者 A_B時，其中A和B為不同的單字，在Google 爬蟲來看的話，若選用A-B，而不選A_B會是因為著？ ->->-> `若選用A_B，只是單方對以A_B這單字作為index和評分上，相較於上者，使用者更難以找得到網站`
<!--SR:!2023-12-28,97,230-->



---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@rcreativeUnderscoreAllowedURL]]
[[@WangZhiUrlsYingGaiYongDuanHengXian]]