## 描述

[[React.memo 比對方式會採用於JS的currProp === prevProp 而衍生出props對應著物件的元件a會因為渲染函式一直邊呼叫邊重建物件而無法讓元件a能夠正常使用memo]]

[[@ithomeDay9ReactHookPianRenShi]]
```jsx
const memoizedCallback = useCallback(
  () => {
    doSomething(a, b);
  },
  [a, b],
);
```

> -   第一個參數是 callback function
> -   第二個參數是一個陣列，此陣列不作為傳到 callback function 的參數
	    -   `useCallback(callback)`: 如果沒有加上這個陣列，每次都會重新執行函式去產生新的函式
	    -   `useCallback(callback, [])`: 空陣列的話，回傳的函式不會改變
	    -   `useCallback(callback, [...someValues])`: 有加上一些元素值的話，當元素值改變時會重新更新回傳的函式

重點：
- 

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React.memo 比對方式會採用於JS的currProp === prevProp 而衍生出props對應著物件的元件a會因為渲染函式一直邊呼叫邊重建物件而無法讓元件a能夠正常使用memo]]
References:
[[@reactHooksAPICanKao]]
[[@ithomeDay9ReactHookPianRenShi]]