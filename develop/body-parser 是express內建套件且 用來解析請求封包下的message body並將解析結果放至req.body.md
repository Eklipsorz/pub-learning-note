## 描述

### body-parser
根據[[@expressExpressBodyparserMiddleware]]所描述：
> Node.js body parsing middleware.
> Parse incoming request bodies in a middleware before your handlers, available under the `req.body`property.

它在Express 4.17前是第三方套件，隨後就內建在Express 框架下，功能有：
- body-parser 本身是一個主要能接收請求封包內的body部分或封包內的body部分並解析成對應結果的middleware
- 當請求經過該middleware時，就會從請求封包內取出body內並經過處理，處理後就將解析結果放至req.body


### body-parser 模組下還具有以下子模組
根據body內容種類的不同，大致上可以區分成：
- 以JSON格式所組成的Body：
- 以URL 編碼表格格式所組成的：以多個key-value pair所組成，每一個key和value都適用URL 編碼(百分比編碼)，若有多個key-value pair會用&相接，比如
```
key1=value1&key2=value2
```

> This module provides the following parsers:
> -   [JSON body parser](http://expressjs.com/en/resources/middleware/body-parser.html#bodyparserjsonoptions)
> -   [URL-encoded form body parser](http://expressjs.com/en/resources/middleware/body-parser.html#bodyparserurlencodedoptions)

若要解析JSON格式的Body，可用JSON body-parser，會如同body-parser將解析結果輸出至req.body，載入方式如下：

```
// app.use若沒指定路徑，就預設為/，並且每當任意請求發送過來就會使用json解析
app.use(express.json())
```


若要解析URL編碼表格格式的Body，可用 URL-encoded form body parser，會如同body-parser將解析結果輸出至req.body，載入方式如下：

```
// app.use若沒指定路徑，就預設為/，並且每當任意請求發送過來就會使用urlencoded解析
app.use(express.urlencoded({ extended: true }))
```

其中extended 是指定

> This option allows to choose between parsing the URL-encoded data with the `querystring` library (when `false`) or the `qs` library (when `true`). The “extended” syntax allows for rich objects and arrays to be encoded into the URL-encoded format, allowing for a JSON-like experience with URL-encoded. For more information,

重點：
- extended 是決定urlencoded套件要用哪個函式庫來解析請求封包，若是false就採用querystring，若是true就採用qs，該函式庫會額外進一步 rich objects和陣列以URL編碼形式來重新編碼。
```
express.urlencoded({ extended: true })
```


## 複習
#🧠 body-parser 是express 框架的套件，其套件用途是做什麼？->->-> `body-parser 本身是一個主要能接收請求封包內的body部分或封包內的body部分並解析成對應結果的middleware，當請求經過該middleware時，就會從請求封包內取出body內並經過處理，處理後就將解析結果放至req.body`
<!--SR:!2023-01-22,55,230-->
#🧠 body-parser 和 express.json 關係是什麼？express.json做啥用？ ->->-> `body-parser是解析請求封包的body，而express.json是body-parser的子模組，負責解析請求封包內的JSON格式body，並回傳解析結果放置req.body`
<!--SR:!2023-02-17,162,250-->
#🧠 body-parser 和 express.urlencoded 關係是什麼? express.urlencoded做啥用？ ->->-> `body-parser是解析請求封包的body，而express.urlencoded是body-parser的子模組，負責解析請求封包內的url編碼表格格式的body，並回傳解析結果放置req.body`
<!--SR:!2023-03-09,174,250-->

#🧠 URL-encoded form body是什麼樣的格式？會用什麼符號來連接 ->->-> `以多個key-value pair所組成，每一個key和value都適用URL 編碼(百分比編碼)來傳送，若有多個key-value pair會用&相接`
<!--SR:!2023-06-13,160,210-->


---
Status: #🌱 
Tags:
[[Express]]
Links:
References:
[[@expressExpressBodyparserMiddleware]]