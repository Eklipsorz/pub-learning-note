


## 描述

> ReactDOM.createRoot => create the main entry point
> 
> the main hook of the overall user interface you are about to build with React That's the idea behind createRoot




### createRoot()

createRoot 是 react-dom 的功能函式：
- 用以建立React層級的Root節點 或者說Virtual DOM節點，其節點會對應著container
- container可以是DOM節點
- 會回傳React層級的Root節點 / Virtual DOM的Root 節點
```
createRoot(container[, options]);
```

Create a React root for the supplied `container` and return the root. The root can be used to render a React element into the DOM with `render`:
```
import ReactDOM from 'react-dom/client'
const root = ReactDOM.createRoot(container);
root.render(element);
```

每個Virtual DOM節點：
- 都對應著實際情況下的DOM節點
- 都具有render方法能夠指定React 層級的 element 放入在對應DOM節點 或者告訴系統 root節點對應的dom節點要如何被渲染


### public/index.html 用途


paths：設定wepback進行前的前置處理
```
appPublic: resolveApp('public'),
appHtml: resolveApp('public/index.html'),
appIndexJs: resolveModule(resolveApp, 'src/index'),
```

webpack.config.js：
```
	new HtmlWebpackPlugin(
		Object.assign(
			{},
			{
				inject: true,
				template: paths.appHtml,
			},
			.
			.
		)
	)
```


CRA 所設定的webpack ：
	- 替前端框架所要參考的模板網頁做處理：但必須安裝html-webpack-plugin
		- 預設為public/index.html，但該html是模板網頁
		- 主要會做將指定的模板網頁和資料合併成HTML、優化、自動加載webpack產生出來的模組

[[html-webpack-plugin 解決了手動定義哪一份文件是要當前端框架的模板網頁以及得替模板文件手動加載webpack處理後的模組檔案]]

由於html-webpack-plugin 預設指定public/index.html為前端框架的模板網頁，好讓前端框架的程式碼能夠對應正確位置的DOM節點。

#### public/index.html 內容
public 下的 index.html是最主要載入bundle.js的html，由index.html來搭配互動來讓bundle.js產生對應的畫面

```
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8" />
		<link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
		<meta name="viewport" content="width=device-width, initial-scale=1" />
		<meta name="theme-color" content="#000000" />
		<meta
			name="description"
			content="Web site created using create-react-app"
		/>
		<link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
		<link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
		<title>React App</title>

	</head>

	<body>
		<noscript>You need to enable JavaScript to run this app.</noscript>
		<div id="root"></div>
	</body>

</html>
```

### src/index.js 總是為webpack的entry?
```
appPublic: resolveApp('public'),
appHtml: resolveApp('public/index.html'),
appIndexJs: resolveModule(resolveApp, 'src/index')
```

若沒特別設定webpack的entry，預設值會是 `./src/index.js`，換言之，一切會以它為主來構成javascript相關模組依賴關係來進行遍歷、轉換，最後整合成數個套件給html載入

接著以index.js和以它為中心的模組依賴關係圖下的模組會綁定在bundle.js來交由模板網頁來載入，剩下則是加載著CSS、圖片

### import
另外import 細節 
1. 若想引入的import是js檔案，可以忽略副檔名，系統會自己檢查
2. 若import 的是其他非JS檔案，如CSS，告知webpack哪些檔案需要被當作模組來處理


CSS-in-JS：一種允許JavaScript能夠解析CSS內容的技術，並讓它透過JavaScript的執行形式來根據執行狀態來更新對應CSS的內容


## 複習
#🧠 React：src/index.js 總是為webpack的entry?->->-> `若沒特別設定webpack的entry，預設值會是 \.\/src\/index.js`
<!--SR:!2024-06-24,413,250-->

#🧠 React：src/index.js 被設定為webpack的entry，那麼具體會做什麼？ ->->-> `一切會以它為主來構成javascript相關模組依賴關係來進行遍歷、轉換，最後整合成數個套件給html載入
<!--SR:!2023-06-15,194,250-->

#🧠 React：src/index.js 被設定為webpack的entry，那麼會模板網頁具體載入什麼？entry本身也會被載入嗎？->->-> `接著以index.js和以它為中心的模組依賴關係圖下的模組會綁定在bundle.js來交由模板網頁來載入，剩下則是加載著CSS、圖片`
<!--SR:!2023-05-17,169,250-->

#🧠 React：完成webpack編譯的網頁會載入到什麼？(共三個) ->->-> `webpack所建立的最後產物-JS產物、CSS、圖片`
<!--SR:!2023-06-10,186,250-->

#🧠 若設定html-webpack-plugin來安裝的話，webpack會對指定的模板網頁做什麼？ ->->-> `主要會將指定模板網頁和指定資料合併成HTML、優化、自動加載webpack所產生出來的模組`
<!--SR:!2023-05-29,181,250-->

#🧠  react-dom 的 createRoot 是什麼樣功能函式？ ->->-> `用以建立React層級的Root節點 或者說Virtual DOM節點`
<!--SR:!2024-01-17,316,250-->

#🧠   react-dom 的 createRoot 會回傳什麼樣的內容 ->->-> `Virtual DOM的Root 節點`
<!--SR:!2024-04-11,369,250-->

#🧠 每一個Virtual DOM的節點會對應著什麼？ ->->-> `都有可能對應著實際情況下的DOM節點`
<!--SR:!2024-07-12,424,250-->


#🧠 每一個Virtual DOM的節點都一定對應著real dom節點？ ->->-> `不一定，具體看操作是否有將(virtual dom)對應畫面渲染在實際上的DOM介面`
<!--SR:!2024-11-19,501,250-->

#🧠 react-dom 的 createRoot(container) 說明一下這什麼樣函式 ->->-> `用以建立React層級的Root節點 或者說Virtual DOM節點，其節點會對應著container、其container可以是DOM節點`
<!--SR:!2025-02-24,555,250-->

#🧠 import 細節：import可以載入CSS嗎？->->-> `主要要看有沒有類似於webpack的套件來負責解析並進行模組處理，有的話就告知該套件來處理；沒的話可能會因無法載入而報錯`
<!--SR:!2023-08-17,177,250-->


#🧠 import 細節：import可以載入CSS嗎？(考量到webpack)->->-> `主要要看有沒有類似於webpack的套件來負責解析並進行模組處理，有的話就告知該套件來處理；沒的話可能會因無法載入而報錯`
<!--SR:!2023-09-14,195,250-->


#🧠 import 細節：若import載入CSS的話，那麼具體會是？ ->->-> `告知webpack哪些檔案需要被當作模組來處理，而CSS則是會以CSS形式來處理`
<!--SR:!2024-02-11,304,250-->


#🧠 import 細節：若載入的是js檔案，可忽略副檔名嗎 ->->-> `可以`
<!--SR:!2023-12-24,111,230-->
#🧠 import 細節：若載入的是css檔案，可忽略副檔名嗎  ->->-> `不可以`
<!--SR:!2024-03-14,351,250-->

#🧠 CSS-in-JS 是什麼樣的技術？->->-> `一種允許JavaScript能夠解析CSS內容的技術，並讓它透過JavaScript的執行形式來根據執行狀態來更新對應CSS的內容`
<!--SR:!2024-12-01,517,250-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React 本身因為react本身支援介面就很多，為了很好專注在不同介面的渲染，所以額外切分react和react-dom]]
[[html-webpack-plugin 解決了手動定義哪一份文件是要當前端框架的模板網頁以及得替模板文件手動加載webpack處理後的模組檔案]]
References: