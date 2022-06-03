
## 描述

### 原生JS的問題
引用[[@node.jsHowUseBuffers]]所描述的原生JS所擁有之問題：
> Pure JavaScript, while great with unicode-encoded strings, does not handle straight binary data very well. This is fine on the browser, where most data is in the form of strings. However, Node.js servers have to also deal with TCP streams and reading and writing to the filesystem, both of which make it necessary to deal with purely binary streams of data.

> One way to handle this problem is to just use strings anyway, which is exactly what Node.js did at first. However, this approach is extremely problematic to work with; It's slow, makes you work with an API designed for strings and not binary data, and has a tendency to break in strange and mysterious ways.

原生JavaScript就設計專門unicode-encode 編碼的字串，當原生JavaScript 要處理TCP/IP封包和檔案內容都先將其內容的二進制0/1資料轉成字串來處理，比如：假如原生資料是如下，那麼轉成字串的話，就會是以result為主
```
// raw data
000000100010001111111
// result
"000000100010001111111"
```

這樣二進制0/1序列構成的字串，就稱之為Binary String[[@mdnBinaryStringsWeb]]

若以字串來處理二進制資料，勢必會比直接用二進制方式處理二進制資料還更多計算成本，若原生JavaScript是在客戶端這樣處理，是可以接受的；但若是在伺服器這樣處理，會徒增更多的成本。

### 隨後的ECMAScript
根據[[@JSZhongDeErJinZhiShuJuChuLiYueFang]]所描述的新規範中：
> ArrayBuffer 對象是 ES6 才納入正式 ECMAScript 規範，是 JavaScript 操作二進制數據的一個接口。ArrayBuffer 對象是以數組的語法處理二進制數據

ECMAScript 有根據上述問題而額外增加ArrayBuffer這個官方標準的API，該API能夠直接處理二進制的資料。

### Node.js 提供的解法
為此，Node.js 就為原生JS提供一套專門處理二進制資料的API，其中API會是以Buffer 類別為主，另外要注意的事情：
- Buffer 類別的API 是隨著Node.js 核心一起出的，並且由Node.js 官方提供的API，並非是ECMAScript上的標準或者原生JS所額外增加的API
- 若沒Node.js，可能得依靠JS目前執行環境是否還擁有直接處理二進制資料的API或者原生ECMAScript是否有提供。

### Node.js Buffer 內部儲存
Buffer 類別的物件會是儲存對應二進制的資料，比如[[multer： 以硬碟來儲存被上傳的檔案 vs 以記憶體來儲存被上傳的檔案]]的例子：

```
buffer: <Buffer 89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52 00 00 01 1a 00 00 00 f2 08 06 00 00 00 92 d3 0a e1 00 00 0c 6a 69 43 43 50 49 43 43 20 50 72 6f 66 69 ... 98994 more bytes>
```

## 複習
#🧠 原生JS的問題如何處理二進制的資料？造成什麼問題 ->->-> `當原生JavaScript 要處理TCP/IP封包和檔案內容都先將其內容的二進制0/1資料轉成字串來處理，若以字串來處理二進制資料，勢必會比直接用二進制方式處理二進制資料還更多計算成本，若原生JavaScript是在客戶端這樣處理，是可以接受的；但若是在伺服器這樣處理，會徒增更多的成本。`
<!--SR:!2022-06-05,12,250-->


#🧠 隨後的ECMAScript 有提出解法來處理二進制資料嗎？ ->->-> `ECMAScript 有根據上述問題而額外增加ArrayBuffer這個官方標準的API，該API能夠直接處理二進制的資料。`
<!--SR:!2022-06-19,18,230-->


#🧠 Node.js 提供的解法有辦法直接處理二進制資料的封包和檔案內容嗎？ ->->-> `Node.js 就為原生JS提供一套專門處理二進制資料的API，其中API會是以Buffer 類別為主`
<!--SR:!2022-07-01,28,250-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Node.js]]
Links:
[[multer： 以硬碟來儲存被上傳的檔案 vs 以記憶體來儲存被上傳的檔案]]
References:
[[@mdnBinaryStringsWeb]]
[[@JSZhongDeErJinZhiShuJuChuLiYueFang]]
[[@huangNodeJsBuffer]]
[[@node.jsHowUseBuffers]]