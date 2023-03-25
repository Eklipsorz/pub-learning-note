## 描述



### optimize code 簡介

optimize code ：
- 具體目標為效能提升
- 手段通常會是minify、refactor、memorized value、code spliting、lazy loading


### lazy-loading 是什麼？

> lazy loading means that we load certain chunks of our code only when that code is needed

lazy loading ：
1. 相對於eager loading的概念
2. 具體為當代碼需要的時候，才會載入該代碼，否則不載入

###  lazy-loading的起因

1. 客戶端要載入的模組是一個單一肥大的模組：預設情況下進行JavaScript模組的建構，會將所有(含元件)模組集中在一個檔案中，有可能使檔案過於龐大而讓客戶端載入效率變差，比如說客戶端想要對應畫面，但必須要先等該檔案下載完成，才能夠讓客戶端進行解析並渲染畫面

2. 客戶端不一定需要所有的服務：客戶端所需要的畫面或者所做的互動不一定需要整個檔案的所有內容，或許只有一小部分會承擔這部分的業務

### lazy loading & code splitting 適用場景

lazy loading & code splitting 適用場景為大型專案、擁有較多元件的專案、準備部署的專案

## 複習

#🧠 react deployment中的optimize code目標為何？ ->->-> `效能提升`
<!--SR:!2023-07-02,117,250-->

#🧠 react deployment中的optimize code目標為效能提升，具體手段為？ ->->-> `minify、refactor、memorized value、code spliting、lazy loading`
<!--SR:!2023-04-01,63,250-->

#🧠  lazy-loading 是什麼？ ->->-> `1. 相對於eager loading的概念 2. 具體為當代碼需要的時候，才會載入該代碼，否則不載入`
<!--SR:!2023-07-03,118,250-->

#🧠 lazy-loading 是具體為當代碼需要的時候，才會載入該代碼，否則不載入，但為何被稱之為lazy? ->->-> `相對於eager loading的概念`
<!--SR:!2023-04-05,65,250-->

#🧠 react：會使用lazy-loading來部署是因爲？ ->->-> `客戶端要載入的模組是一個單一肥大的模組、客戶端不一定需要所有的服務`
<!--SR:!2023-04-16,74,250-->

#🧠  react：會使用lazy-loading來部署是因爲客戶端要載入的模組是一個單一肥大的模組，那麼具體是為了什麼？？ ->->-> `預設情況下進行JavaScript模組的建構，會將所有(含元件)模組集中在一個檔案中，有可能使檔案過於龐大而讓客戶端載入效率變差`
<!--SR:!2023-04-13,20,210-->


#🧠 react：會使用lazy-loading來部署是因爲客戶端要載入的模組是一個單一肥大的模組，那麼具體會是預設情況下進行JavaScript模組的建構，會將所有(含元件)模組集中在一個檔案中，有可能使檔案過於龐大而讓客戶端載入效率變差，請舉例說明 ->->-> `客戶端想要對應畫面，但必須要先等該檔案下載完成，才能夠讓客戶端進行解析並渲染畫面`
<!--SR:!2023-04-13,72,250-->


#🧠  react：會使用lazy-loading來部署是因爲客戶端不一定需要所有的服務，那麼具體會是什麼？？ ->->-> `客戶端所需要的畫面或者所做的互動不一定需要整個檔案的所有內容，或許只有一小部分會承擔這部分的業務`
<!--SR:!2023-04-16,74,250-->

#🧠  lazy loading & code splitting 適用場景為何？ ->->-> `lazy loading & code splitting 適用場景為大型專案、擁有較多元件的專案、準備部署的專案`
<!--SR:!2023-04-12,70,250-->

#🧠 lazy loading 需要splitting會為什麼？  ->->-> `將模組切分成好幾塊，以利根據所需來載入`
<!--SR:!2023-06-29,96,230-->
`




---
Status: #🌱 
Tags:
[[React]]
Links:
[[react 部署步驟：test code -> optimize code -> build app for production -> upload -> configure server]]
References: