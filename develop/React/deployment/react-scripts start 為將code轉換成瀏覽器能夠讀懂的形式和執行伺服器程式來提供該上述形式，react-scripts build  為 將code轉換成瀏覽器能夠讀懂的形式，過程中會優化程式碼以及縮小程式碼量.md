
## 描述

## react-scripts
> This package includes scripts and configuration used by Create React App.
> Please refer to its documentation:


重點：
- react-scripts 是CRA裡頭用來建構React App的程式




### react-scripts start 指令作用
npm run start => react-scripts start
1. 將code轉換成瀏覽器能夠讀懂的形式
2. 執行伺服器程式來提供該上述形式

細節：
1. 在這不做優化手段


### react-scripts build 指令作用
npm run build => react-scripts build
1. 將code轉換成瀏覽器能夠讀懂的形式，過程中會優化程式碼以及使產出程式碼的量減少

  
細節：
1. 在這裡不執行伺服器來提供結果網頁

### build 目錄存放
1. 存放npm run build/react-script build建構出來的代碼和目錄
2. 若要架設伺服器來提供對應網頁，就將build目錄的所有內容轉移至伺服器中
3. 不建議在裡頭更改，因爲隨時會因為build而更新

  
/build/static：
1. 包含優化過的CSS代碼、JS代碼

## 複習

#🧠  react-scripts 是CRA裡頭是做什麼？->->-> ` react-scripts 是CRA裡頭用來建構React App的程式`
<!--SR:!2023-02-02,28,250-->

#🧠 react-scripts start 指令作用為何？->->-> `1. 將code轉換成瀏覽器能夠讀懂的形式 2. 執行伺服器程式來提供該上述形式`
<!--SR:!2023-01-05,10,250-->

#🧠 react-scripts start 指令作用為1. 將code轉換成瀏覽器能夠讀懂的形式 2. 執行伺服器程式來提供該上述形式，請問形式還會優化嗎 ->->-> `並不會`
<!--SR:!2023-02-02,28,250-->


#🧠  react-scripts build 指令作用為何？ ->->-> `將code轉換成瀏覽器能夠讀懂的形式，過程中會優化程式碼以及使產出程式碼的量減少`
<!--SR:!2023-02-02,28,250-->

#🧠 react-scripts build 指令作用為將code轉換成瀏覽器能夠讀懂的形式，過程中會優化程式碼以及使產出程式碼的量減少，請問還會啟動伺服器程式嗎 ->->-> `並不會`
<!--SR:!2023-02-02,28,250-->


#🧠 react-scripts build 指令作用 vs  react-scripts start 指令作用為何？->->-> `皆會產出瀏覽器能夠讀懂的形式，前者會進一步優化，後者並不會；前者並不會啟動伺服器來提供最後結果網頁，後者則會啟動伺服器來提供最後結果網頁`
<!--SR:!2023-01-05,10,250-->


#🧠  react：build 目錄存放什麼->->-> `存放npm run build/react-script build建構出來的代碼和目錄`
<!--SR:!2023-02-02,28,250-->

#🧠 react：執行完畢npm run build之後，那要如何將程式碼轉移至伺服器？ ->->-> `就將build目錄的所有內容轉移至伺服器中`
<!--SR:!2023-01-11,6,230-->

#🧠 react：/build/static存放什麼？ ->->-> `存放優化過的CSS代碼、JS代碼`
<!--SR:!2023-01-26,23,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
References: