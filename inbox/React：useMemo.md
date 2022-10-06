## 描述

[[@ithomeDay8ReactHookPianRenShi]]
> `const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);`

> -   第一個參數是 callback function
> -   第二個參數是一個陣列，此陣列不作為傳到 callback function 的參數
>    -   `useMemo(computation)`: 如果沒有加上這個陣列，每次都會重新執行函式去產生新的值
>    -   `useMemo(computation, [])`: 空陣列的話，回傳值不會改變
>    -   `useMemo(computation, [...someValues])`: 有加上一些元素值的話，當元素值改變時會重新更新函式回傳值




[[@reactHooksAPICanKao]]
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

> 回傳一個 memoized 的值。

> 傳遞一個「建立」function 及依賴 array。useMemo 只會在依賴改變時才重新計算 memoized 的值。這個最佳化可以避免在每次 render 都進行昂貴的計算。




重點：
-


###  useMemo 什麼時候執行觸發
[[@reactHooksAPICanKao]]
> 要謹記傳到 `useMemo` 的 function 會在 render 期間執行。不要做一些通常不會在 render 期間做的事情。例如，處理 side effect 屬於 `useEffect`，而不是 `useMemo`。

重點：
- useMemo 在對應元件的render function執行時，才會被執行

## 複習


---
Status: #🌱 
Tags:
Links:
References:
[[@ithomeDay8ReactHookPianRenShi]]
[[@reactHooksAPICanKao]]