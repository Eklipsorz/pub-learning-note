
## 描述


### 載入資料來渲染所需要注意的情況

根據資料載入狀況(沒進行、進行中、完成)和是否有初始渲染資料可以分為四種情況

1. 沒進行載入資料且沒初始渲染資料來渲染的情況
2. 沒進行載入資料且有初始渲染資料來渲染的情況
3. 載入資料進行中且初始渲染資料為任意的情況
4. 載入資料完成且有初始資料渲染為任意的情況


在這

### 載入資料至

在載入資料至以資料來渲染畫面之間的時間差若過多的話，可以添加loading spinner或者載入效果來增加使用者體驗(告知使用者要渲染的資料正在處理)


若要呈現正在載入的文字，流程會是

1. 先在元件下註冊isLoading這狀態

`const [isLoading, setIsLoading] = useState(false);`

  

2. 然後在處理載入資料的程式模組前一行添加setState以及處理載入資料的程式模組後一行添加setState
```
1.  setIsLoading(true)
2.  // 載入資料處理
3.  setIsLoading(false)
```


3. 在渲染部分，根據isLoading是否為true來調整畫面

if we're not loading, but we've got no movies yet,

若我們還沒載入資料，但就是現在還沒有資料呈現的話，比如在一開始時渲染


## 複習



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用Fetch API 來發送請求來獲取資料並渲染]]
References: