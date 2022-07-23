


## 描述

> 在上面的內容有提到說，瀏覽器物件模型有著階層性的架構，最上層便是Window物件，代表著瀏覽器視窗本身，若是視窗中含有框架，則每個框架都還有屬於自己的window物件。

> 所有的BOM都可透過window來存取。window物件的使用不須經過宣告，可以直接使用。事實上，在Javcascript中，所有的全域變數、函式、物件，其實都是屬於window物件。舉例來說：

```
<script>
x=5;
alert (window.x); //輸出 5
</script>
```


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags: 
[[JavaScript]]
Links:
[[HTML 的script 能夠允許瀏覽器邊解析DOM邊執行對應的程式碼，通常為JS，每個文件都會有各自的JS全域執行環境]]

References: