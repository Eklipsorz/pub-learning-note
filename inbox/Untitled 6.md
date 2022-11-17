## 描述

### Query String
[[@wikidataQueryString2022]] 所描述
> A **query string** is a part of a uniform resource locator (URL) that assigns values to specified parameters

> Typical URL containing a query string is as follows:

> `https://example.com/over/there?name=ferret`

> When a server receives a request for such a page, it may run a program, passing the query string, which in this case is `name=ferret`, unchanged to the program. The question mark is used as a separator, and is not part of the query string

重點：
- query string 是用來向特定伺服器索要特定資源的請求字串，以URL形式來表示，比如：
`https://example.com/over/there?name=ferret`
- query string 在客戶端和伺服器之間會以百分比編碼或者URL編碼



### 
Query string

1. 參數形式：以問號開頭的key value pair

2. 本身可以被特定路由處理器給攔截到


### 

應用：

1. 接收參數來對指定項目做排序


###
至做排序清單項目的功能：

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

useLocation

1. react-router-dom的hook

2. 該hook 會回傳location object，而該物件夾帶著目前載入的頁面所擁有的資訊(含URL部分)



###
history.push & replace的隱患

1. 若頻繁對stack的最上面元素做push和replace，會使react不斷執行unmount 和 mount，即使是一直push相同頁面的網址，也會不斷執行unmount 和 mount

###
> new URLSearchParams()
> The `**URLSearchParams**` interface defines utility methods to work with the query string of a URL.

1. 一個介面，專門協助開發者處理特定URL上的query string：

流程：先找到其URL的query string部分->擷取query string->將query string按照key-value pair來轉換成對應物件來讓該介面很好操作

2. 具體含有屬性和數個方法

3.  內建於瀏覽器

  

其中Query String



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References: