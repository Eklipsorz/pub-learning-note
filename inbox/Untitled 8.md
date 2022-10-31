## 描述

對於分配URL至多個頁面/服務的方式，具體有：
- 基於 static URL的分配：分配固定URL給每個頁面或者服務
- 基於dynamic URL 的分配：憑藉著頁面/服務所對應的URL是經過處理才能對應的特性，就拿能夠代表每個頁面和服務的識別字或者特徵來作為參數，並且讓處理方根據特徵、其頁面/服務所需的資料、模板網頁來回傳對應頁面/服務，即為根據識別字來生成對應頁面/服務，不需手動來填入固定URL

### Dynamic Route with Params


```
<Route path="/xxx1/:something">
	...
</Route>
```


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[URL都泛指著特定頁面或服務所會對應的URL，其URL對應關係是否會依據著請求處理方的處理執行狀況而產生對應關係，而分成Dynamic URL或者Static URL]]
References: