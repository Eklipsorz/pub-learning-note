## body parser

1. 它本身是一個middleware function，用來解析request object所包含的Message Body並轉換成伺服器可讀取的形式，該形式會另外替middleware function用上的request物件增加一個新屬性-body，而新屬性值為內容轉換後的內容。

  

2. body parser 在Express 4.17之前是第三方套件，隨後就內建在Express，且body parser本身能解析不同形式的內容，其中一個最知名的是解析URL編碼，在這裏內建的function 是如下，其中options會是option物件，用來設計解析過程如何實現，option物件較常使用的屬性為extended，這是用指定解析URL 編碼的函式庫是什麼，若是true的話，就是指定qs 函式庫，若是false的話，就是指定querystring函式庫

  

```
express.urlencoded([options])
```



> This option allows to choose between parsing the URL-encoded data with the `querystring` library (when `false`) or the `qs` library (when `true`). The “extended” syntax allows for rich objects and arrays to be encoded into the URL-encoded format, allowing for a JSON-like experience with URL-encoded. For more information,

重點：
- extended 是決定urlencoded套件要用哪個函式庫來解析請求封包，若是false就採用querystring，若是true就採用qs，該函式庫會額外進一步 rich objects和陣列以URL編碼形式來重新編碼。
```
express.urlencoded({ extended: true })
```