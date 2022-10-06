## 描述

```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

> 回傳一個 memoized 的值。

> 傳遞一個「建立」function 及依賴 array。useMemo 只會在依賴改變時才重新計算 memoized 的值。這個最佳化可以避免在每次 render 都進行昂貴的計算。

> 要謹記傳到 `useMemo` 的 function 會在 render 期間執行。不要做一些通常不會在 render 期間做的事情。例如，處理 side effect 屬於 `useEffect`，而不是 `useMemo`。



## 複習


---
Status: #🌱 
Tags:
Links:
References:
