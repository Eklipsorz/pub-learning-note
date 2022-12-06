## 描述

對於分配URL至多個頁面/服務的方式，具體有：
- 基於 static URL 的分配：分配固定URL給每個頁面或者服務，通常會是手動配置URL和頁面/服務之間的關係
- 基於 dynamic URL 的分配：憑藉著頁面/服務所對應的URL是經過處理才能對應的特性，就拿能夠代表每個頁面和服務的識別字或者特徵來作為參數，並且讓處理方根據特徵、其頁面/服務所需的資料、模板網頁來回傳對應頁面/服務，即為根據識別字來生成對應頁面/服務，不需手動配置URL和頁面/服務之間的關係

### 基於 static URL 的分配 vs. 基於 dynamic URL 的分配
- URL對應關係：
	- 前者的URL對應關係必須手動分配； 後者的URL對應關係會按照請求處理方來決定對應
- 其URL對應關係會不會受到請求處理方而改變
	- 前者的URL對應關係不受到請求處理方而改變；後者的URL對應關係會受到請求處理方而改變
### 基於dynamic URL 的分配

- 以Path版本的正規表達式來擷取滿足表達式的內容作為參數處理：
	- 常見會是以下面形式來擷取：在這裡的固定路徑會是xxx1，專擷取著/xxx1/為開頭的任意語句，並把xxx1/後頭的內容擷取出來，並存放至名為something的空間或者變數
```
/xxx1/:something 
```

以react-router-dom為例子：
```
<Route path="/xxx1/:something">
	<Component1 />
</Route>
```


#### 如何讓Component1 取得something

- 以固定路徑來擷取參數處理


```
import { useParams } from 'react-router-dom';

const Component1 = (props) => {
	const obj = useParams();
}
```

### useParams
[[@react-routerReactRouterDeclarativea]]
> useParams

> useParams returns an object of key/value pairs of URL parameters. Use it to access match.params of the current \<Route\>.

重點：
- useParams 是react-router-dom提供的自製hook，主要會回傳離它較近的Parent Route元件所獲取到的URL 參數資訊
- useParams 會挑選離它較近的Parent Route元件來擷取
- 基於dynamic URL 的分配下的方式來獲取URL 參數--以Path版本的正規表達式來擷取滿足表達式的內容作為參數處理
- URL parameters 資訊會以 物件 來存放，屬性名稱會是Route 元件使用正規表達式擷取內容用的變數名稱，屬性值則是使用變數名稱對應的內容
- 用法為
	- useParams 會回傳URL parameters 資訊物件
```
import { useParams } from 'react-router-dom';
const params = useParams();
```





#### 案例

當使用者輸入以下內容時，
```
/xxx1/abc/efg
```

會因為Route關係而將abc擷取出來存放在something1這屬性，efg也同樣被擷取，只是按照位置和指定名稱而存放在something2這屬性，最後構成以下代表目前取出來URL parameters 資訊的物件

```
{
	something1: abc,
	something2: efg
}
```


接著被Route component 包裹的Component1使用useParams時，就擷取URL parameters 資訊的物件。
```
<Route path="/xxx1/:something1/:something2">
	<Component1 />
</Route>

--------------

import { useParams } from 'react-router-dom';

const Component1 = (props) => {
	const obj = useParams();
}
```



## 複習

#🧠 對於分配URL 至多個頁面/服務的方式，具體有哪些？->->-> `基於 static URL 的分配、基於 dynamic URL 的分配`
<!--SR:!2023-01-02,32,230-->

#🧠 對於分配URL至多個頁面/服務的方式， 基於 static URL 的分配是什麼樣？ ->->-> `通常會是手動配置URL和頁面/服務之間的關係`
<!--SR:!2022-12-07,16,230-->

#🧠 對於分配URL至多個頁面/服務的方式， 基於 static URL 的分配是分配固定URL給每個頁面或者服務，通常會如何做？？ ->->-> `通常會是手動配置固定URL至每個頁面/服務`
<!--SR:!2022-12-13,28,250-->

#🧠  對於分配URL至多個頁面/服務的方式， 基於 dynamic URL 的分配是->->-> `憑藉著頁面/服務所對應的URL是經過處理才能對應的特性，就拿能夠代表每個頁面和服務的識別字或者特徵來作為參數，並讓處理方根據特徵的對應處理結果來回傳其頁面和服務`
<!--SR:!2022-12-12,27,250-->

#🧠 對於分配URL至多個頁面/服務的方式， 基於 dynamic URL 的手段會是什麼？ ->->-> `以Path版本的正規表達式來擷取滿足表達式的內容作為參數處理`
<!--SR:!2023-02-03,59,250-->

#🧠 對於分配URL至多個頁面/服務的方式，基於 static URL 的分配 vs. 基於 dynamic URL 的分配 最大差別是什麼？ ->->-> `1. 前者的URL對應關係必須手動分配 2. 其URL對應關係不受到請求處理方而改變； 1. 後者的URL對應關係會按照請求處理方來決定對應 2. 其URL對應關係會受到請求處理方而改變`
<!--SR:!2023-01-07,40,230-->


#🧠 對於分配URL至多個頁面/服務的方式， 基於 dynamic URL 的手段會是以Path版本的正規表達式來擷取滿足表達式的內容作為參數處理，舉例 ->->-> `/xxx1/:something，在這裡的固定路徑會是xxx1，專擷取著/xxx1/為開頭的任意語句，並把xxx1/後頭的內容擷取出來，並存放至名為something的空間或者變數 `
<!--SR:!2022-12-12,27,250-->


#🧠 useParams  是React 內建hook嗎？還是什麼？ ->->-> `不是內建，而是react-router-dom所提供的自製hook`
<!--SR:!2022-12-12,27,250-->

#🧠 react-router-dom：useParams是什麼？做什麼？  ->->-> `主要會回傳離它較近的Parent Route所獲取到的URL 參數資訊`
<!--SR:!2023-01-13,43,249-->

#🧠 react-router-dom：useParams會獲取哪一種Route元件所截取的URL parameters？ ->->-> `useParams 會挑選離它較近的Parent Route元件來擷取`
<!--SR:!2023-01-11,42,249-->


#🧠 react-router-dom：useParams是基於什麼樣的基礎(什麼樣分配下的方式)來擷取URL parameters ->->-> `基於 dynamic URL 的分配中，以Path版本的正規表達式來擷取滿足表達式的內容作為參數處理`
<!--SR:!2022-12-13,28,250-->

#🧠 react-router-dom：useParams是會擷取包裹著目前component的Route component 所獲得的 URL parameters 資訊，這裡的資訊是如何表示？ ->->-> `物件，屬屬性名稱會是Route 元件使用正規表達式擷取內容用的變數名稱，屬性值則是使用變數名稱對應的內容`
<!--SR:!2022-12-06,23,250-->

#🧠 react-router-dom：useParams 語法為？ ->->-> `import { useParams } from 'react-router-dom'; const params = useParams();`
<!--SR:!2022-12-10,26,250-->

#🧠 react-router-dom：useParams 回傳什麼？ ->->-> `useParams 會回傳URL parameters 資訊物件`
<!--SR:!2022-12-12,27,250-->

#🧠 當使用者輸入以下內容時：\/xxx1\/abc\/efg，如何在Component1擷取到\<Route path="\/xxx1\/\:something1\/\:something2\"\> \<Component1 \/\> \<\/Route\> 和abc和efg？->->-> `import { useParams } from 'react-router-dom'; const Component1 = (props) => {  const obj = useParams(); }`
<!--SR:!2023-01-26,54,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[URL都泛指著特定頁面或服務所會對應的URL，其URL對應關係是否會依據著請求處理方的處理執行狀況而產生對應關係，而分成Dynamic URL或者Static URL]]
[[named parameters 或 named argument 是指作為參數來進行特定處理的內容，其內容會以特定名稱來命名標記，以便能在處理時方便辨認]]
References:
[[@react-routerReactRouterDeclarativea]]