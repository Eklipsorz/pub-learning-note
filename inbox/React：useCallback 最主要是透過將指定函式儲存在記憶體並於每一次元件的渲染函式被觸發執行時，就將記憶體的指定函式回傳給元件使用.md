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
- useCallback 最主要是透過將指定函式儲存在記憶體並於每一次元件的渲染函式被觸發執行時，會檢測依賴是否變動來將儲存記憶體內的指定函式回傳給元件使用，這解決了：
	- 由props對應著物件的元件A會因為JS原生比對問題以及每一次渲染函式被呼叫就重建物件而導致元件A的props比對結果都不一樣，進而無法正常使用memo
- useCallback 如同名稱那樣，會專門儲存一個特定function作為以後方便執行用
- 語法：
	- 第一個參數會是以特定function為結構來產生對應function的callback，callback內會儲存一個基本函式-baseFunction 並搭配著 第二個參數-依賴項目
	- 第二個參數會是依賴項目所構成的陣列，決定是否執行callback 來以baseFunction為主衍生出新函式
	- 回傳值會是baseFunction為主的新函式物件
		- 若deps 為空陣列，就會被系統認定不會被改變的依賴項目，回傳的函式物件就會以目前最新的baseFunction來回傳，而不執行裡頭的callback來衍生出以baseFunction為主的新函式
		- 若沒添加\[deps\]，就會被系統認定為一直被改變的依賴項目，回傳的函式物件就會直接執行裡頭的callback來衍生出以baseFunction為主的新函式
		- 若添加\[a, b\]，會先判斷a或者b是否有任一變動，有變動才執行對應callback來衍生baseFunction為主的新函式來回傳；沒變動就不執行，直接回傳目前最新的baseFunction
```
const callbackResult = useCallback(baseFunction, [a, b])
```
記得更改baseFunction

```
const callbackResult = useCallback(callback, [deps])
```


### useCallback 何時檢查並觸發？
[[@vencovskyAnswerWhenUse2019]]

> useCallback
> On every render, everything that's inside a functional component will run again.

重點：
- 每一次執行元件的render函式就會執行useCallback，並檢查useCallback所依賴的內容是否有變動。

### function 被儲存在哪？

基本上會儲存在React 體系下內部的儲存區塊


## 複習


---
Status: #🌱 #📝
Tags:
[[React]]
Links:
[[React.memo 比對方式會採用於JS的currProp === prevProp 而衍生出props對應著物件的元件a會因為渲染函式一直邊呼叫邊重建物件而無法讓元件a能夠正常使用memo]]

References:
[[@reactHooksAPICanKao]]
[[@ithomeDay9ReactHookPianRenShi]]