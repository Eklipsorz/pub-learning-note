## 描述

React：create-react-app 專案下的npm run command

[[@facebookAvailableScriptsCreate]] 所描述：


> `npm start` ： Runs the app in the development mode.


`npm run build`：Builds the app for production to the `build` folder. It correctly bundles React in production mode and optimizes the build for the best performance.
`npm run eject`
[[React的create-react-app 預設會隱藏與開發無關的檔案和無用的模組安裝依賴關係，若要停止隱藏就執行npm run eject]]


重點：
- npm run start/ npm start：啟動開發用的網頁伺服器，一開始伺服器就會先對目前專案做webpack優化，接著只要客戶端對伺服器發送指令，然後再將優化結果回傳給客戶端。
	細節：
		- 若原始碼有變動的話，會同等更新伺服器上的內容。
- npm run build：利用webpack來產出部署狀態下的套件(HTML、CSS、JS)並放置build目錄
- npm run eject：將CRA隱藏的檔案和模組依賴關係重新注入至目前CRA當前建立的環境

## 複習
#🧠 React： npm run start/ npm start  是什麼？ ->->-> `啟動開發用的網頁伺服器，一開始伺服器就會先對目前專案做webpack優化，接著只要客戶端對伺服器發送指令，然後再將優化結果回傳給客戶端。`

#🧠 React： 啟動npm run start/ npm start後，若原始碼有變動的話，會有什麼反應？->->-> `若原始碼有變動的話，會同等更新伺服器上的內容`

#🧠 React： npm run build 是什麼？ ->->-> `利用webpack來產出部署狀態下的套件(HTML、CSS、JS)並放置build目錄`

#🧠 React： npm run build 是什麼？->->-> `將CRA隱藏的檔案和模組依賴關係重新注入至目前CRA當前建立的環境`

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React的create-react-app 預設會隱藏與開發無關的檔案和無用的模組安裝依賴關係，若要停止隱藏就執行npm run eject]]
References:
[[@facebookAvailableScriptsCreate]]