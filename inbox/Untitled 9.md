## 描述


###

optimize code 步驟：

具體目標為效能提升，手段通常會是refactor、memorized value、code spliting、lazy loading


###


lazy loading means that we load certain chunks of our code only when that code is needed

lazy loading ：

1. 相對於eager loading的概念

2. 具體為當代碼需要的時候，才會載入該代碼，否則不載入

###


預設情況下進行JavaScript模組的建構，會將所有(含元件)模組集中在一個檔案中，有可能使檔案過於龐大而讓客戶端載入效率變差，比如說客戶端想要對應畫面，但必須要先等該檔案下載完成，才能夠讓客戶端進行解析並渲染畫面

  

再加上客戶端所需要的畫面或者所做的互動不一定需要整個檔案的所有內容，或許只有一小部分會承擔這部分的業務

###
lazy loading & code splitting 適用場景為大型專案、擁有較多元件的專案


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: