

## 描述

```
<a href="/todos/{{ todo._id }}/edit">edit</a> (已编辑)
上面這是對的 (已编辑)
    
<a href="./todos/{{ todo._id }}/edit">edit</a>
但這是錯的。出現 Cannot GET /todos/todos/619fa11736bb3556219423ee/edit
```

./todos 和 ./todos 是兩種不同的定位方法
    
    
前者是告訴瀏覽器請到/ 目錄下的todos
    
    
後者是說請以目前所在的目錄來找到todos
    
    
前者是absolute path 絕對路徑，白話一點就是你告訴瀏覽器資源的詳細所在
    

後者就是relative path 相對路徑，白話一點就是你以某個東西為參考來說明位置，比如學校旁邊的便利商店，學校就是參考位置 (已编辑)
    
    
首先當你發送GET /todos/:id請求至伺服器端 (已编辑)
    
    
 瀏覽器的確會如你所料來發送
    
    
但它本身會為了暫存網頁內容以及方便處理，會採用儲存檔案的形式來儲存將每個請求回應，分別轉換成目錄和檔案，位置處理方式也是基於瀏覽器認定的檔案架構來處理，識別方式也很簡單，大部分是看端點是否還能包含其他端點，若能包含就是目錄，比如todos/:id就表示todos包含:id，所以就會把todos認為是目錄，那麼id的部分就會以檔案來當作，其內容會是GET /todos/:id。 不過這識別方式只是其中之一，具體還是要看瀏覽器如何實現轉換 (已编辑)
    

所以當你拿到GET /todos/:id 回應時，瀏覽器會順勢幫你建立名為在根目錄（localhost:3000/)下建立一個todos目錄


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664897762/blog/browser/actual-source_z1unb7.png)


此時，你在GET /todos/:id的結果網頁點擊按鈕的話，就等同於是在/todos/:id檔案下進行按鈕點擊
    
    
而你的按鈕會指向./todos/:id/....，而你目前所瀏覽的畫面會是在根目錄下的todos目錄的某個檔案 (已编辑)
    
那麼瀏覽器就會認為你想以/todos這個目錄作為參考位置，來找到它底下的另一個todos子目錄下的:id....
    
也就是認為你想到/todos/todos/:id......
    
另外目錄=資料夾


## 複習


---
Status: #🌱 
Tags:
Links:
References: