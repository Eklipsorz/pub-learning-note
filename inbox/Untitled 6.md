## 描述



### Query string
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]

由於使用特定符號來區隔：一邊為伺服器端點；另一邊為query string，所以本身可以被任意特定路由處理器給攔截到。


### Query string 應用

應用：

1. 接收參數來對指定項目做排序


####
製作排序清單項目的功能：
- 將排序邏輯部分分到資料業務邏輯那
- 再將處理後的資料放到渲染層面

  
渲染層面若要添加排序按鈕的話，可以為按鈕的點擊事件添加

1. 將使用者以programatic navigation 方式來從目前頁面轉移至其他頁面所在網址

    - 網址會是/quotes?sort=xxxx：添加query string的形式來重新對該端點發送請求，讓他們接收到參數來排序資料，然後再把資料放到渲染層面




###

1. 將使用者以programatic navigation 方式來從目前頁面轉移至其他頁面所在網址

- 網址會是/quotes?sort=xxxx：添加query string的形式來重新對該端點發送請求，讓他們接收到參數來排序資料，然後再把資料放到渲染層面



實現會是如下，其中sorting會是變數，並以此來依據執行過程來決定排序方式，而非寫死

`'/quotes?sort=' + sorting`


### 





###
history.push & replace的隱患

1. 若頻繁對stack的最上面元素做push和replace，會使react不斷執行unmount 和 mount，即使是一直push相同頁面的網址，也會不斷執行unmount 和 mount






## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
[[query string 會以URL的特定部分作為其內容，通常會搭配問號來作為區隔。問號左半邊為伺服器端點；右半邊為query string的區段部分。主要是來向特定伺服器索要特定資源的請求字串]]
[[QueryString 加號問題 - 伺服器在解析query參數時就會自動以無UTF8形式來解碼，其+被解出來會是空白]]
[[URLSearchParams 是內建於瀏覽器並以JS而撰寫的介面，專門協助開發者處理特定URL上的query string]]
References:
