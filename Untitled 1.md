


## 描述

> ReactDOM.createRoot => create the main entry point
> 
> the main hook of the overall user interface you are about to build with React That's the idea behind createRoot




### createRoot()

createRoot 是 react-dom 的功能函式：
- 用以建立React層級的Root節點 或者說Virtual DOM節點，其節點會對應著container
- container可以是DOM節點
- 會回傳React層級的Root節點
```
createRoot(container[, options]);
```

Create a React root for the supplied `container` and return the root. The root can be used to render a React element into the DOM with `render`:
```
import ReactDOM from 'react-dom/client'
const root = ReactDOM.createRoot(container);
root.render(element);
```

每個Virtual DOM節點都具有render方法能夠指定React 層級的 element 放入在對應DOM節點 或者告訴系統 root節點對應的dom節點要如何被渲染




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




### import
另外import 細節  
1. 若想引入的import是js檔案，可以忽略副檔名



CSS-in-JS：一種允許JavaScript能夠解析CSS內容的技術，並讓它透過JavaScript的執行形式來根據執行狀態來更新對應CSS的內容


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React 本身因為react本身支援介面就很多，為了很好專注在不同介面的渲染，所以額外切分react和react-dom]]
References: