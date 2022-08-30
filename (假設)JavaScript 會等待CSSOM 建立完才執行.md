## 描述

[[@ithome30TianXueHuiWeb]]
> 前面提到 Javascript 會阻擋 DOM 的建構，很神奇的是，CSS 會阻擋 Javascript 的執行。讓我們繼續以前例說明（不過增加了一段 jQuery）。


> 假設兩個 JS file 都抵達了，然而 CSS file 還沒到的話，瀏覽器一樣只能傻傻等待，為什麼呢?各位仔細看就會發現第二個 JS 修改了 id=first 的 p tag 的 CSS 屬性，原本 CSS 裡面設定它的文字顏色是紅色，後來被 JS 改成藍色。這一段 JS 很單純，但會操作 CSSOM ，瀏覽器還沒抓完 CSS 自然無法建構 CSSOM ， CSSOM 都還沒建好，JS 怎麼可能操作它呢?

> 看到這邊你有沒有發現 HTML 、 Javascript 以及 CSS 三者間微妙的關係了呢？

> 1.  Javascript 會阻擋 DOM 的建構
> 2.  CSS 會阻擋 Javascript 的執行
> 3.  CSS 會影響頁面的 Rendering

> 上面第二、第三點加起來，更加凸顯讓瀏覽器盡快取得 CSS file 的重要性。



### 案例1：CSSOM 

```
  <link href="layout.css" rel="stylesheet" type="text/css" />
  <script src="http://code.jquery.com/jquery-1.11.0.min.js"></script>
  <script src="script.js" />


  <p id="first">Hello this is a test page.</p>
```

> CSS file 的內容：
```
p {
  color: red;
}
```

> JS file 的內容：
```
$(document).ready(function(){
  $("#first").css("color","blue");
});
```




## 複習





---
Status: #🌱 
Tags:
[[JavaScript]] - [[CSS]]
Links:
References:
[[@ithome30TianXueHuiWeb]]