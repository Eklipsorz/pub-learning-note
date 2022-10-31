## 描述


> \<NavLink\>

> A special version of the \<Link\> that will add styling attributes to the rendered element when it matches the current URL.

we often want to highlight the active link in the navigation

-> NavLink 本質上是以Link元件，只是會用特定樣式來顯示目前頁面是屬於哪個Link

> ## [activeClassName: string](https://v5.reactrouter.com/web/api/NavLink/activeclassname-string)

> The class to give the element when it is active. The default given class is `active`. This will be joined with the `className` prop.

重點：
- NavLink 在react-router中是一個component，主要是以Link元件為基礎來提示目前頁面是屬於哪個Link component
- 本質是Link 元件，只是多了一些樣式來渲染
- 常見用法為
	- to：指定要導向哪個頁面，具體會以瀏覽器的absolute URL和 relative URL規範所定義的root path為主
	- activeClassName：則是指定當Link 元件為active element時就將對應DOM節點的class設定class-name
	- xxxx1 則是被綁定頁面連結的hypertext
```
<NavLink to="xxx" activeClassName="class-name"> xxxx1 </NavLink>
```
## 複習


---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
References: