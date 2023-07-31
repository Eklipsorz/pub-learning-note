## 描述



### 每個effect hook皆為獨立的

當元件處於mounting時，就會建立對應effect hook函式物件來綁定在該元件，並觸發effect，隨後若發生updating或者unmounting的話，預設上會再去觸發effect。

若同一個元件因為viewport的畫面切換而發生unmount並重新發生mounting，在發生unmount 就會移除舊有effect，並於mounting時期會再次產生額外的effect hook來綁定在該元件，觸發如同上述那樣


### 當畫面A被切換成畫面B時
當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B，在這裡可分為：
- 畫面A 和 畫面B 都是畫面A
- 畫面A 和 畫面B 都不一樣

## 複習

#🧠 React：若同一個元件因為viewport的畫面切換而發生unmount並重新發生mounting，請問會如何保留新舊的hook? ->->-> `在發生unmount 就會移除舊有effect，並於mounting時期會再次產生額外的effect hook來綁定在該元件，觸發如同上述那樣`
<!--SR:!2024-11-06,476,250-->
`

#🧠 React：當畫面A被切換成畫面B時，unmounting 和 mounting會是如何？ ->->-> `當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B`
<!--SR:!2024-11-04,474,250-->

#🧠 React：當畫面A被切換成畫面B時，即為畫面A發生unmounting，並且mounting 畫面B，請問畫面A可以是畫面B一樣嗎？->->-> `- 畫面A 和 畫面B 都是畫面A - 畫面A 和 畫面B 都不一樣`
<!--SR:!2024-10-22,462,250-->

---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References: