## 描述

[[@mdnNavigationSectionElement]]

> The \<nav\> HTML element represents a section of a page whose purpose is to provide navigation links, either within the current document or to other documents. Common examples of navigation sections are menus, tables of contents, and indexes.
```
<nav class="menu">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```


重點：
- navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向。
	- 其他頁面會是指應用程式內部的頁面 或者 其他外部網頁
- navigation 區塊語法：該語法會被瀏覽器中給定預設樣式、預設事件處理
```
<nav>
....
</nav>
```
- navigation 常見的配置：
	- 清單 (ul、ol)
	- 清單項目(每個項目會含有anchor element) (li)
	- anchor element (a)
```
<nav class="menu">
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

### navigation 意義

> the act of directing a ship, aircraft, etc. from one place to another, or the science of finding a way from one place to another

重點
- navigation：將特定事物在一個地方A被地方A的任意事物引導至指定地方的行為、過程、方式，而非單純從一個地方A移動至指定地方。



## 複習

#🧠 navigation 意義 是什麼？(行為、過程、方式，請強調引導) ->->-> `將特定事物在一個地方A被地方A的任意事物引導至指定地方的行為、過程、方式`
<!--SR:!2024-12-13,467,250-->

#🧠 navigation 意義 是單純從一個地方A移動至指定地方嗎？(行為、過程、方式) 為什麼？->->-> `將特定事物在一個地方A被地方A的任意事物引導至指定地方的行為、過程、方式，因爲還強調帶有由那個特定地方的任意事物引導事物至特定地方`
<!--SR:!2024-10-09,421,250-->

#🧠 navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，舉一個例子來單純說明navigation 這行為？ ->->-> `使用者在特定頁面A點擊頁面中的按鈕，就到達特定頁面B`
<!--SR:!2023-12-15,94,230-->


#🧠 navigation 意義 是什麼？->->-> `將特定事物在一個地方A的任意事物給引導至指定地方的行為、過程、方式`
<!--SR:!2024-06-13,345,250-->


#🧠 navigation 在網頁上會是什麼元素？不是標籤，請強調引導->->-> `navigation 是網頁用來幫助使用者在一個頁面下被該頁面下的元件導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向`
<!--SR:!2024-02-12,273,250-->


#🧠  navigation是網頁用來幫助使用者導向其他頁面的區塊，會由什麼元素所構成？ 不考慮常用 ->->-> `具體區塊內會含有多個hyperlink給予使用者做互動來導向`
<!--SR:!2024-07-11,365,250-->

#🧠 navigation是網頁用來幫助使用者導向其他頁面的區塊，能轉移的頁面會是什麼？ ->->-> `其他頁面會是指應用程式內部的頁面 或者 其他外部網頁`
<!--SR:!2024-10-11,423,250-->

#🧠 navigation是網頁用來幫助使用者導向其他頁面的區塊，常見會搭配什麼元素？ ->->-> `	- 清單 (ul、ol) - 清單項目(每個項目會含有anchor element) (li) - anchor element (a)`
<!--SR:!2023-12-14,98,230-->

#🧠 以HOME、ABOUT這兩個hyperlink為例子，請用navigation元素來打造 ->->-> ``
<!--SR:!2024-07-25,373,250-->

#🧠 navigation是網頁用來幫助使用者導向其他頁面的區塊，對應元件為何？ ->->-> `<nav>`
<!--SR:!2023-10-25,197,230-->

#🧠 navigation是網頁用來幫助使用者導向其他頁面的區塊，對應元件的用法為何？->->-> `<nav> .... </nav>`
<!--SR:!2025-02-02,499,250-->

#🧠 navigation是網頁用來幫助使用者導向其他頁面的區塊，瀏覽器會替它增加什麼東西？ ->->-> `預設樣式、預設事件處理`
<!--SR:!2024-12-12,466,250-->



---
Status: #🌱 
Tags:
[[HTML]]
Links:
[[header 是一個網頁元素，主要會以網頁畫面上的頂部區塊呈現引導使用者進入應用程式的區塊]]
References:
[[@mdnNavigationSectionElement]]
