## 描述

### component 

最佳實踐為每一個檔案各為一個component，並統一存放在src/components下目錄

#### component 檔名
檔名會以upper camel case為主

#### component file內的函式名稱
1. 函式名稱會和檔名一致
2. upper camel case為主

#### 為何要採取upper case版本camel
為了很好地區分出哪個才是原生HTML和自製的component：
	- 若原生HTML會以小寫為主
	- 若自製的會以大寫為主

### App.js
> App.js is root Component
> 
> 1. which means it's main Component being rendered here in our starting file in index.js
>2. all our components will be either nested inside of App.js or nested inside of our components

重點：
- App.js 是Virtual DOM中的根節點，最一開始會被渲染的檔案
- 其他所有元件將會在App.js來構築巢狀結構或者在其他元件上構築巢狀結構




## 複習
#🧠 React：component的最佳實踐是什麼？ ->->-> `每一個檔案各為一個component`

#🧠 React：component會集中存放在哪？->->-> `src/components`

#🧠 React： component 檔名會是以什麼命名法為主？->->-> `upper camel case為主`
<!--SR:!2022-08-23,10,250-->

#🧠 React：component file內的函式名稱會是以什麼命名法為主 ->->-> `1. 函式名稱會和檔名一致、upper camel case為主`
<!--SR:!2022-08-23,10,250-->

#🧠 React：為何要採取upper case版本camel來命名component ->->-> `為了很好地區分出哪個才是原生HTML和自製的component：	- 若原生HTML會以小寫為主 - 若自製的會以大寫為主`
<!--SR:!2022-08-20,7,250-->


#🧠 React：App.js 是什麼樣的檔案，對於Virtual DOM來說 ->->-> `App.js 是Virtual DOM中的根節點，最一開始會被渲染的檔案`
<!--SR:!2022-08-23,10,250-->



---
Status: #🌱 
Tags:
[[JavaScript]] - [[React]]
Links:
[[React - 可使用function 和 class 來建構react component]]
References: