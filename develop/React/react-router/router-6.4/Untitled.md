## 描述


### request 物件的formData
request object 本身是用fetch api 而建立的。



其中request object的 formData方法是  
- 以非同步形式來執行

- 從裡頭接收請求封包中的body部分並轉換成FormData object



> The formData() method of the Request interface reads the request body and returns it as a promise that resolves with a FormData object.

  

FormData Object

  

The FormData interface provides a way to easily construct a set of key/value pairs representing form fields and their values, which can then be easily sent using the fetch() or XMLHttpRequest.send() method.


### 處理表格資料(action)的端點
1. 與表格所在端點一樣的端點，但http動詞會是與獲取表格畫面的http動詞會是不同：
	 - post 為 轉遞表格資料並處理
	 - get 為 獲取表格畫面
2. 與表格所在的端點不一樣的端點



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: