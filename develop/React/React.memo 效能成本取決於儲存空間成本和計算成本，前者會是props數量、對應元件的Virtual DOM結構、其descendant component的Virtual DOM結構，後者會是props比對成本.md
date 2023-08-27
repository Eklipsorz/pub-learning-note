## 描述


### React.memo 效能成本取決於

效能成本取決於
- 空間成本：
	- props 數量 (含props.chilrden本身)
	- 對應元件的Virtual DOM結構 (複雜度)
	- descendant component的Virtual DOM結構 (複雜度)
- 計算成本：
	- props 比對，最主要會是比對 目前props資訊和記憶體儲存的props資訊是否一樣

#### 為什麼全部元件都不套用memo ? 


> why aren't we using that on all components

> if it allow use to optimize them and it's impossible to say which cost is higher because it depends on the number of props you have and on the complexity of your component and number of child components your component has

首先React.memo本身處理起來是有基本的時間和空間成本，若貿然不管元件是否會頻繁更改內容，那麼很有可能會因props時常改變的元件而浪費成本，因為
- 沒辦法獲取到memo的好處
- 在沒獲得到好處的情況下，多做memo本身的成本


## 複習


#🧠 React.memo的效能成本是取決於什麼？ ->->-> `空間成本、計算成本`
<!--SR:!2024-03-28,325,250-->

#🧠 React.memo的效能成本是空間成本、計算成本，其中空間成本是什麼？ ->->-> `	- props 數量 (含props.chilrden本身) - 對應元件的Virtual DOM結構 (複雜度) - descendant component的Virtual DOM結構 (複雜度)`
<!--SR:!2024-08-20,414,250-->


#🧠 React.memo的效能成本是空間成本、計算成本，其中計算成本是什麼？  ->->-> `props 比對，最主要會是比對 目前props資訊和記憶體儲存的props資訊是否一樣`
<!--SR:!2023-07-20,179,250-->

#🧠 為什麼全部元件都不套用React.memo ->->-> `首先React.memo本身處理起來是有基本的時間和空間成本，若貿然不管元件是否會頻繁更改內容，那麼很有可能會因props時常改變的元件而浪費成本`
<!--SR:!2023-12-07,102,230-->

#🧠 為什麼全部元件都不套用React.memo ？首先React.memo本身處理起來是有基本的時間和空間成本，若貿然不管元件是否會頻繁更改內容，那麼很有可能會因props時常改變的元件而浪費成本，為何會說是浪費？ ->->-> `- 沒辦法獲取到memo的好處 - 在沒獲得到好處的情況下，多做了memo本身的成本`
<!--SR:!2025-01-06,508,250-->




---
Status: #🌱  
Tags:
[[React]]
Links:
[[React：React.memo 將特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function]]
References: