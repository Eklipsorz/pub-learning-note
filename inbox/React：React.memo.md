## 描述

[[@reactReactDingCengAPI]]
> React.memo 是一個 higher order component。

> 如果你的 function component 每次得到相同 prop 的時候都會 render 相同結果，你可以將其包在 React.memo 之中，透過快取 render 結果來在某些情況下加速。這表示 React 會跳過 render 這個 component，並直接重用上次的 render 結果。

> React.memo 只會確認 props 的改變。如果你的 function component 被 wrap 在 React.memo 內，實作中具有一個 useState、useReducer 或 useContext Hook，當 state 或 context 改變時，它仍然會持續 rerender。

> 這預設只會對 prop 進行 shallow compare 。如果你需要控制比較的方法，你可以提供一個自訂的比較 function 作為第二個參數。

```
function MyComponent(props) {
  /* render using props */
}
function areEqual(prevProps, nextProps) {
  /*
  return true if passing nextProps to render would return
  the same result as passing prevProps to render,
  otherwise return false
  */
}
export default React.memo(MyComponent, areEqual);
```


重點：
- React.memo 如字面上的意思，會將擁有特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中
	- 當發生渲染並且要準備執行指定元件A的渲染函式時，會透過特定規則來檢查是否達到標準
		- 預設特定規則會是 **目前傳遞至元件A的props 資訊是否與緩存儲存的props資訊一樣的**
		- 若達到的話，就直接回傳緩存或者記憶體中的元件A之對應Virtual DOM
		- 若沒達到的話，就直接執行指定元件A的渲染函式以此來得到對應元件的Virtual DOM，並且
- 語法會是
```
React.memo(component)
```



It tells React that for this component which it get as a argument,

- React should look at the props this component gets and check the new value for all those props and compare it to the previous value those props got

- And only if the value of a prop changed, the component should be re-executed and re-evaluated.

- And if the parent component changed but the props values for that component here did not change, component execution will be skipped

  

React.memo(component)

- 當它正要被觸發渲染函式時，會檢查其props是否有變動，有變動才會執行對應渲染函式，否則就不執行



React.memo

- This is for functional components, allow us to optimize functional components

- For class-based components, this does not work.


tell React that is should only re-execute this DemoOutput component under certain circumstances：

- circumstances would be that props, which this component received, changed

### memorize 命名緣由
[[@wikidataMemorization2022]]
> Memorization is the process of committing something to memory.

重點：
- Memorization 是一個提交特定事物並永久儲存在記憶體的行為或者過程
- Memorize 則是提交特定事物並永久儲存在至記憶體

## 複習



---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：higher-order-component 是指專門以component function C 為參數作為處理並產出component function B為結果的 component function A]]
References:
[[@wikidataMemorization2022]]
[[@reactReactDingCengAPI]]