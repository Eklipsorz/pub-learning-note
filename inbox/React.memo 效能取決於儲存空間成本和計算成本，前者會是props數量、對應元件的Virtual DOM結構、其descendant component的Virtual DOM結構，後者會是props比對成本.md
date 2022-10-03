## 描述


### React.memo 效能取決於

效能成本取決於
- 儲存成本：
	- props 數量 (含props.chilrden本身)
	- 對應元件的Virtual DOM結構 (複雜度)
	- descendant component的Virtual DOM結構 (複雜度)
- 計算成本：
	- props 比對，最主要會是比對 對應元件所擁有的props 數量

#### 為什麼全部元件都不套用memo ? 


> why aren't we using that on all components

> if it allow use to optimize them and it's impossible to say which cost is higher because it depends on the number of props you have and on the complexity of your component and number of child components your component has

首先React.memo本身處理起來是有基本的時間和空間成本，若貿然不管是否以不同的props來渲染著對應元件，那麼很有可能會因props時常改變的元件而浪費成本，因為
- 沒辦法獲取到memo的好處
- 在沒獲得到好處的情況下，浪費了memo本身的成本


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：React.memo 將特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function]]
References: