## 描述

### link 標籤
[[@w3schoolHTMLLinkTag]]
> The `<link>` tag defines the relationship between the current document and an external resource.

> href : specifies the location of the linked document
> 	- value: URL
> 
> rel ：Required. Specifies the relationship between the current document and the linked document
> 	- value : 

```
	alternate  
	author  
	dns-prefetch  
	help  
	icon  
	license  
	next  
	pingback  
	preconnect  
	prefetch  
	preload  
	prerender  
	prev  
	search  
	stylesheet
```



重點：
- link 是HTML內容的標籤之一
- 主要用來定義目前文件與目前檔案以外的資源之間的關係是如何並載入至目前文件
- 主要使用的屬性(attribute)為rel、href
	- rel：定義要以什麼形式來將額外資源載入至目前文件上，會以字串來表示
	- href：定義額外資料所在，會以網址來表示

#### 可載入什麼？
[[@w3schoolHTMLLinkTag]]
> The \<link\> tag is most often used to link to external style sheets or to add a favicon to your website.

> rel ：Required. Specifies the relationship between the current document and the linked document
> 	- value : 

```
	alternate  
	author  
	dns-prefetch  
	help  
	icon  
	license  
	next  
	pingback  
	preconnect  
	prefetch  
	preload  
	prerender  
	prev  
	search  
	stylesheet
```
重點：
- link 標籤 可以載入stylesheet

### 引入CSS檔案

```
<link rel="stylesheet" href="xxxx">
```


### 同一個DOM文件出現指定重複樣式的對應內容

當同一個DOM文件出現指定重複樣式的對應內容
- 同個css檔案出現重複樣式，而DOM文件載入css檔案
	```
	// 檔案1
	.test {
		width: 100px;
		height: 20px;
		border-color: aqua;
	}
	
	.test {
		width: 10000px;
	}
	```
- 不同個css檔案出現重複樣式，而DOM文件載入css檔案1和css檔案2
	```
	// 檔案1
	.test {
		width: 100px;
		height: 20px;
		border-color: aqua;
	}
	// 檔案2
	.test {
		width: 10000px;
	}
	```

結果皆為
```
	// 檔案1
	.test {
		height: 20px;
		border-color: aqua;
		width: 10000px;
	}
```

其結果會因為：
- 由於會使用相同的CSSOM，這使得它會採用css specificity來決定每個declaration的去留

## 複習
#🧠 HTML：link 標籤是什麼？->->-> `主要用來定義目前文件與目前檔案以外的資源之間的關係是如何並載入至目前文件`
<!--SR:!2022-09-19,18,250-->

#🧠 HTML：link 標籤的rel 屬性是什麼？->->-> `定義要以什麼形式來將額外資源載入至目前文件上，會以字串來表示`
<!--SR:!2022-09-04,10,250-->

#🧠 HTML：link 標籤的href 屬性是什麼？ ->->-> `定義額外資料所在，會以網址來表示`
<!--SR:!2022-09-04,10,250-->


#🧠 HTML ：link標籤時常載入哪些檔案？ ->->-> `css、圖片`
<!--SR:!2022-09-04,10,250-->

#🧠 HTML ：link標籤如何載入CSS檔案 ->->-> `<link rel="stylesheet" href="xxxx">`
<!--SR:!2022-09-04,10,250-->

#🧠 同個css檔案出現重複樣式，而DOM文件載入css檔案，其test樣式為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661091574/blog/cssTag/a-css-inside-same-dom_hptxjr.png) ->->-> `.test { height: 20px; border-color: aqua; width: 10000px;}`
<!--SR:!2022-09-20,19,250-->
#🧠 不同個css檔案出現重複樣式，而DOM文件載入css檔案，其test樣式為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661091574/blog/cssTag/two-css-inside-same-dom_gumjxf.png) ->->-> `.test { height: 20px; border-color: aqua; width: 10000px;}`
<!--SR:!2022-09-02,8,250-->
`


#🧠 同一個DOM文件出現指定重複樣式的對應內容，為何CSS會將![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661091574/blog/cssTag/a-css-inside-same-dom_hptxjr.png)解析成![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661091574/blog/cssTag/css-inside-same-dom-result_vhks4m.png)->->-> `由於會使用相同的CSSOM，這使得它會採用css specificity來決定每個declaration的去留`
<!--SR:!2022-09-03,3,250-->




#🧠 CSS從上至下去定義每個樣式會有什麼內容，當遇到重複樣式，就會與過去樣式的對應內容合併，會如何合併 ->->-> `同樣樣式屬性，就以最新檔案的屬性值為主；不同樣式屬性：就直接合併`
<!--SR:!2022-09-04,10,250-->




---
Status: #🌱 
Tags:
[[CSS]]
Links:
References:
[[@w3schoolHTMLLinkTag]]