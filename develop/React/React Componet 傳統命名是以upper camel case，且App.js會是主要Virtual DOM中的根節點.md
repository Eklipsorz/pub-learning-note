## 描述

### component 

最佳實踐為每一個檔案各為一個component，並統一存放在src/components下目錄

#### component 檔名
檔名會以upper camel case為主

#### component file內的函式名稱
1. 函式名稱會和檔名一致
2. upper camel case為主

#### 為何要採取upper case版本camel

> If you meant to render a React component, start its name with an uppercase letter.
- React 要求自製的component名稱之首字必須是大寫，若貿然使用會被React系統阻止渲染
- 其目的是為了很好地區分原生HTML標籤和自製的component
	- 若以小寫首字的話，React會以瀏覽器內建的解析器來做，若解析不到就報錯
	- 若以大小首字的話，React會以自己體系的解析器來做，若解析不到就報錯
- 錯誤警告案例：

錯誤訊息
```
index.js:1 Warning: The tag <basicform> is unrecognized in this browser. If you meant to render a React component, start its name with an uppercase letter.
    at basicform
    at div
    at App
```
原始碼
```
import basicform from "./components/BasicForm";

function App() {
  return (
    <div className='app'>
      <basicform />
    </div>
  );
}
```

除此之外，React並沒有要求Component名稱一定要Upper Case Camel，只是基於首字大寫的基礎下，開發者而額外延伸使用的命名法則



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
<!--SR:!2022-12-07,74,250-->

#🧠 React：component會集中存放在哪？->->-> `src/components`
<!--SR:!2022-12-07,74,250-->

#🧠 React：React為什麼要求自製的component名稱之首字必須是大寫？ ->->-> `為了很好地區分原生HTML標籤和自製的component`

#🧠 React：React要求自製的component名稱之首字必須是大寫，那麼自製元件首字小寫還能渲染嗎？ 為什麼->->-> `並不能，具體會先以瀏覽器內建的解析器來解析，若解析不到就報錯`

#🧠 React：React要求自製的component名稱之首字必須是大寫，那麼原生元件首字大寫還能渲染嗎？ 為什麼->->-> `並不能，具體會先以React會以自己體系的解析器來做，若解析不到就報錯`


#🧠 React：React 面對component名稱之首字必須是大小寫會分別做哪些處理？？->->-> `	- 若以小寫首字的話，React會以瀏覽器內建的解析器來做 - 若以大小首字的話，React會以自己體系的解析器來做`


#🧠 React： 在滿足元件首字為大寫的基礎下，component 檔名會是以什麼命名法為主？->->-> `upper camel case為主`
<!--SR:!2022-11-10,57,250-->

#🧠 React：在滿足元件首字為大寫的基礎下，component file內的函式名稱會是以什麼命名法為主 ->->-> `1. 函式名稱會和檔名一致、upper camel case為主`
<!--SR:!2022-11-16,61,250-->


#🧠 React：App.js 是什麼樣的檔案，對於Virtual DOM來說 ->->-> `App.js 是Virtual DOM中的根節點，最一開始會被渲染的檔案`
<!--SR:!2022-11-21,65,250-->



---
Status: #🌱 
Tags:
[[JavaScript]] - [[React]]
Links:
[[React - 可使用function 和 class 來建構react component]]
References: