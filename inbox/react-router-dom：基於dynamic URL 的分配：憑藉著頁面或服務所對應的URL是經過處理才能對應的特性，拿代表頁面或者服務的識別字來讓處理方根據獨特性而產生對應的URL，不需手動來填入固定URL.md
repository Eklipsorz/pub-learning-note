## 描述

對於分配URL至多個頁面/服務的方式，具體有：
- 基於 static URL的分配：分配固定URL給每個頁面或者服務
- 基於dynamic URL 的分配：憑藉著頁面/服務所對應的URL是經過處理才能對應的特性，就拿能夠代表每個頁面和服務的識別字或者特徵來作為參數，並且讓處理方根據特徵、其頁面/服務所需的資料、模板網頁來回傳對應頁面/服務，即為根據識別字來生成對應頁面/服務，不需手動來填入固定URL

### 基於dynamic URL 的分配

- 以固定路徑來擷取參數處理：在這裡的固定路徑會是xxx1，專擷取著/xxx1/為開頭的任意語句，並把xxx1/後頭的內容擷取出來，並存放至名為something的空間或者變數
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
- useParams 是react-router-dom提供的自製hook，主要會擷取包裹著目前component的Route component 所獲得的 URL parameters 資訊
- URL parameters 資訊會以key-value pairs 或者 物件 來存放，key/屬性名稱會是Route 元件使用:xxxx的xxxx為主，value/屬性值則是使用:xxxx 擷取到的內容
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


---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
[[URL都泛指著特定頁面或服務所會對應的URL，其URL對應關係是否會依據著請求處理方的處理執行狀況而產生對應關係，而分成Dynamic URL或者Static URL]]
References:
[[@react-routerReactRouterDeclarativea]]