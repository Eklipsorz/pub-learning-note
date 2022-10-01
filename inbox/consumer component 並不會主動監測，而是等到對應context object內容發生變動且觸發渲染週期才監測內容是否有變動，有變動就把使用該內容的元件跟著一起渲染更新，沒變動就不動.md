## 描述



### 當對應context object的內容發生更動時
當對應context object的內容發生更動時：
	- 若執行能夠觸發渲染週期的話，每個使用context object存放狀態的元件A會因為consumer component監測到有變動，而因而觸發元件A的渲染；若沒有變動的話，不會觸發元件A的渲染
	- 若沒執行能夠觸發渲染週期的話，會因爲沒觸發執行各個元件的渲染，而不會讓每個使用context object存放狀態的元件A而觸發。

### consumer component 什麼時候才監測



當對應context object的內容發生更動時：
	- 若執行能夠觸發渲染週期的話，每個使用context object存放狀態的元件A擁有consumer component才會監測
	- 若沒執行夠觸發渲染週期的話，每個使用context object存放狀態的元件A擁有consumer component不會監測
	- 不會主動監測

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: