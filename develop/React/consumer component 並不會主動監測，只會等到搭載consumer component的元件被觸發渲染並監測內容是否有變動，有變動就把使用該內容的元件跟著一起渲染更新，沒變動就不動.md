## 描述



### 當對應context object的內容發生更動時
當對應context object的內容發生更動時：
	- 若執行能夠觸發渲染週期的話，每個使用context object存放狀態的元件A會因為consumer component監測到有變動，而因而觸發元件A的渲染；若沒有變動的話，並不會存取context object內容，並直接以目前資訊來渲染元件
	- 若沒執行能夠觸發渲染週期的話，會因爲沒觸發執行各個元件的渲染，而不會讓每個使用context object存放狀態的元件A而觸發。

### consumer component 什麼時候才監測

當對應context object的內容發生更動時：
	- 若執行能夠觸發渲染週期的話，每個使用context object存放狀態的元件A擁有consumer component才會監測
	- 若沒執行夠觸發渲染週期的話，每個使用context object存放狀態的元件A擁有consumer component不會監測
	- 不會主動監測

#### 總結
- 特定context object 的 consumer component 並不會主動監測，只會等到搭載consumer component的元件被觸發渲染才開始監測
- 監測時會檢查對應context object內容是否有變動，有變動才真正讓搭載consumer component的元件去使用新內容來更新渲染；沒變動不會更新搭載consumer component的元件

## 複習
#🧠 React：搭載 consumer component 的元件 什麼時候才監測 ->->-> `只會等到搭載consumer component的元件被觸發渲染`
<!--SR:!2023-08-02,190,250-->

#🧠 React：consumer component 的元件 監測功能是主動監測？還是挑情況 ->->-> `並不會主動監測，而是看條件觸發`
<!--SR:!2023-12-23,102,230-->

#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，會做什麼 ->->-> `若執行能夠觸發渲染週期的話，每個使用context object存放狀態的元件A會因為consumer component監測到有變動，而因而觸發元件A的渲染；若沒有變動的話，並不會存取context object內容，並直接以目前資訊來渲染元件`
<!--SR:!2025-02-03,526,250-->

#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，且檢測到context object沒變動的話，會做什麼？ ->->-> `若沒有變動的話，並不會存取context object內容，並直接以目前資訊來渲染元件`
<!--SR:!2023-05-30,79,250-->
<!--SR:!2023-08-04,191,250-->

#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，且檢測到context object沒變動的話，會做什麼？ ->->-> `若沒有變動的話，並不會存取context object內容，並直接以目前資訊來渲染元件`
<!--SR:!2023-05-30,79,250-->

#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，且檢測到context object變動以及沒變動的話，會是如何？ ->->-> `檢測對應context object 內容是否有變動，有變動才真正讓搭載consumer component的元件去使用新內容來更新渲染；若沒有變動的話，並不會存取context object內容，並直接以目前資訊來渲染元件`
<!--SR:!2023-06-04,82,250-->


#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，且檢測到context object變動的話，會做什麼？ ->->-> `搭載其consumer component的元件會觸發渲染，因而取得最新context內容來渲染`
<!--SR:!2023-08-07,194,250-->

#🧠 React：搭載 consumer component 的元件中，若consumer component功能開始觸發的話，且檢測到context object變動的話，搭載其consumer component的元件會用什麼更新自己元件內容->->-> `主要會用context object內容`
<!--SR:!2025-01-28,520,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: