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
- 主要用來定義目前文件與目前檔案以外的資源之間的關係是如何
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

其結果會因為CSS解析方式

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[CSS]]
Links:
References:
[[@w3schoolHTMLLinkTag]]