## 描述



[[@mdnURLSearchParamsWebAPIs]]
> new URLSearchParams()
> The `**URLSearchParams**` interface defines utility methods to work with the query string of a URL.


> The URLSearchParams() constructor creates and returns a new URLSearchParams object.
```
new URLSearchParams(options)
```

> `options` Optional

> One of:
> -   A string, which will be parsed from `application/x-www-form-urlencoded` format. A leading `'?'` character is ignored.

> # URLSearchParams.get()
> The get() method of the URLSearchParams interface returns the first value associated to the given search parameter.


```
get(name)
```
> `name`
> The name of the parameter to return.

重點：
- 一個內建於瀏覽器並以JS而撰寫的介面
- 該介面是專門協助開發者處理特定URL上的query string
	- 流程：
		1. 先找到其URL的query string部分
		2. 擷取query string
		3. 將query string按照key-value pair來轉換成對應物件來讓該介面很好操作
- 具體含有屬性和數個方法來操作攔截到的query string
	- 建構式：專門將指定的query string轉換成query string物件
		- options 指定要轉換的query string是什麼
		- 回傳query string 物件
		```
		new URLSearchParams(options)
	   ```
	- URLSearchParams.get()：以指定的參數名數來回傳它第一個找到的參數值
		- name：要擷取的參數名稱
		```
	  URLSearchParams.get(name)
	   ```

## 複習


#🧠 URLSearchParams 是什麼？用途是什麼？ ->->-> `一個內建於瀏覽器並以JS而撰寫的介面，該介面是專門協助開發者處理特定URL上的query string`
<!--SR:!2023-03-12,72,250-->

#🧠 URLSearchParams 是個內建於瀏覽器並以JS而撰寫的介面，其介面是做什麼？ ->->-> `該介面是專門協助開發者處理特定URL上的query string`
<!--SR:!2023-03-13,73,250-->

#🧠 URLSearchParams 是個內建於瀏覽器並以JS而撰寫的介面，其介面是做協助開發者處理特定URL上的query string，具體會如何協助，流程是？->->-> `		1. 先找到其URL的query string部分 2. 擷取query string 3. 將query string按照key-value pair來轉換成對應物件來讓該介面很好操作`
<!--SR:!2023-02-26,63,250-->

#🧠 URLSearchParams 是個內建於瀏覽器並以JS而撰寫的介面，它含有什麼？(屬..方)->->-> `屬性和數個方法來操作攔截到的query string`
<!--SR:!2023-02-27,64,250-->

#🧠  URLSearchParams 建構式用法是什麼->->-> `new URLSearchParams(options)`
<!--SR:!2023-02-28,64,250-->

#🧠 URLSearchParams 建構式是做什麼？ ->->-> `專門將指定的query string轉換成query string物件`
<!--SR:!2023-03-06,68,250-->

#🧠 URLSearchParams 建構式用法是new URLSearchParams(options)，回傳會是什麼？ ->->-> `回傳query string 物件`
<!--SR:!2023-03-09,70,250-->

#🧠 URLSearchParams 建構式用法是new URLSearchParams(options)，options會是什麼？ ->->-> `指定要轉換的query string是什麼`
<!--SR:!2023-03-05,68,250-->


#🧠 URLSearchParams.get()會是做什麼？ ->-> `以指定的參數名數來回傳它第一個找到的參數值`

#🧠 URLSearchParams的get用法是什麼？ ->->-> `URLSearchParams.get(name)`
<!--SR:!2023-03-01,65,250-->


#🧠 URLSearchParams.get(name)會是以指定的參數名數來回傳它第一個找到的參數值，其中name會是？？ ->->-> `要擷取的參數名稱`
<!--SR:!2023-03-14,73,250-->



---
Status: #🌱 
Tags: 
[[HTML]] - [[JavaScript]]
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
References:
[[@mdnURLSearchParamsWebAPIs]]