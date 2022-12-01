## 描述
[[@mdnWindowWebAPIs]] 所描述

>  The Window interface represents a window containing a DOM document; the document property points to the DOM document loaded in that window.

重點：
- Window 物件是指顯示 **特定文件所渲染出來的畫面** 的顯示區塊物件
- 每個window物件只會呈現 一個 特定DOM Document所載入的畫面。



### window 命名緣由
[[@WindowComputing2022]] 所描述：
> In computing, a window is a graphical control element. It consists of a visual area containing some of the graphical user interface of the program it belongs to and is framed by a window decoration.

重點：
- window 是一個圖型化控制元件
- window 主要包含一個可視化的區塊以及搭配線條來描述區塊的範疇，該區塊會存在多個程式的使用者圖形化介面。

## 複習
#🧠 在電腦科學裡，window是什麼？ ->->-> `是一個圖型化控制元件，主要包含一個可視化的區塊以及搭配線條來描述區塊的範疇，該區塊會存在多個程式的使用者圖形化介面`
<!--SR:!2023-02-07,113,250-->

#🧠 瀏覽器的Window 物件是什麼？ ->->-> `Window 物件是指顯示 **特定文件所渲染出來的畫面** 的顯示區塊物件`
<!--SR:!2023-05-27,180,250-->

#🧠 瀏覽器的多個文件的渲染畫面會是共享同一個window物件嗎？ ->->-> `並不是，每個文件的渲染畫面都各為一個window物件`
<!--SR:!2023-06-13,194,250-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Operating System]]
Links:
References:
[[@mdnWindowWebAPIs]]
[[@WindowComputing2022]]