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
- 該介面是專門協助開發者以物件的形式來處理query string。
- 具體含有屬性和數個方法來操作攔截到的query string
	- 建構式：專門將指定的query string轉換成query string物件
		- options 為字串，URL的query string部分
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


#🧠 http://xxxx/path?key1=xxx1&key2=xxx2 中，其中的key1和key2的key-value pair會是甚麼? (請說出兩種別名)->->-> `query string`
<!--SR:!2023-09-23,23,250-->

#🧠 query string 和 URL parameters之間的差別是甚麼? ->->-> `前者是以問號開頭的key-value pairs作為參數；後者則是以URL格式下的特定path做為placeholder來當作成參數，並從placeholder所在的位置取出確定內容`
<!--SR:!2023-10-02,20,230-->

#🧠 URLSearchParams 是什麼？用途是什麼？ ->->-> `一個內建於瀏覽器並以JS而撰寫的介面，該介面是專門協助開發者以物件的形式來處理query string`
<!--SR:!2023-09-27,17,248-->


#🧠 URLSearchParams 是個內建於瀏覽器並以JS而撰寫的介面，其介面是做什麼？ ->->-> `該介面是專門協助開發者以物件的形式來處理query string`
<!--SR:!2023-09-22,14,248-->


#🧠 URLSearchParams 是個內建於瀏覽器並以JS而撰寫的介面，它含有什麼？(屬..方)->->-> `屬性和數個方法來操作攔截到的query string`
<!--SR:!2023-11-21,82,230-->

#🧠  URLSearchParams 建構式用法是什麼->->-> `new URLSearchParams(options)`
<!--SR:!2023-09-27,17,248-->


#🧠 URLSearchParams 建構式是做什麼？ ->->-> `專門將指定的query string轉換成query string物件`
<!--SR:!2023-09-22,14,248-->


#🧠 URLSearchParams 建構式用法是new URLSearchParams(options)，回傳會是什麼？ ->->-> `特定query string內容之 物件`
<!--SR:!2023-09-26,16,248-->


#🧠 URLSearchParams 建構式用法是new URLSearchParams(options)，options會是什麼？ ->->-> `指定要轉換的query string是什麼`
<!--SR:!2023-09-25,15,248-->

#🧠 new URLSearchParams('http://host/path?khttp://host/path?key1=value1ey1=value1') 能夠正常作用嗎? 為何->->-> `並不能，因為該介面僅能夠將query string格式的字串轉換成query string物件`
<!--SR:!2023-09-26,16,246-->

#🧠 new URLSearchParams('http://host/path?key1=value1').get('key1')是甚麼? 為何->->-> `null，因為該介面僅能夠將query string格式的字串轉換成query string物件`
<!--SR:!2023-09-29,19,246-->


#🧠 URLSearchParams.get()會是做什麼？ ->-> `以指定的參數名數來回傳它第一個找到的參數值`

#🧠 URLSearchParams的get用法是什麼？ ->->-> `URLSearchParams.get(name)`
<!--SR:!2023-11-08,83,230-->


#🧠 URLSearchParams.get(name)會是以指定的參數名數來回傳它第一個找到的參數值，其中name會是？？ ->->-> `要擷取的參數名稱`
<!--SR:!2025-01-04,473,250-->



---
Status: #🌱 
Tags: 
[[HTML]] - [[JavaScript]]
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
References:
[[@mdnURLSearchParamsWebAPIs]]