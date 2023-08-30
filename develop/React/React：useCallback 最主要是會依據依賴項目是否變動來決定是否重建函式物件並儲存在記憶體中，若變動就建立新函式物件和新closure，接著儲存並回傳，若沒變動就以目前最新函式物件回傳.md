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
- useCallback本身是一個內建Hook，註冊在元件上
- useCallback 最主要是會依據依賴項目是否變動來決定是否重建函式物件並儲存在記憶體中，若變動就建立新函式物件和新closure，接著儲存並回傳，若沒變動就以目前記憶體的最新函式物件來回傳，這解決了：
	- 解決memo本身的重建問題：每一次渲染函式被呼叫就重建物件(函式物件)，將這些物件搭載至特定元件A的props，會因為物件在reference value上會是不一樣而導致元件A的props比對結果都不一樣，進而無法正常使用memo
- useCallback 如同名稱那樣，會專門建立並儲存一個特定function來作為特定情況下要使用的函式
- 語法： 
	- 第一個參數是用函式物件來定義每一次所建立的函式物件之基本函式架構-baseFunction
	- 第二個參數會是依賴項目所構成的陣列，決定是否要在基本函式架構baseFunction搭配目前的依賴項目來建立新的函式物件，其函式物件會擁有新的closure
	- 回傳值會是根據\[deps\]來決定回傳新函式物件或者記憶體儲存的函式物件，其函式物件會夾帶closure，該closure的識別字會是特定執行時機下的記憶體區塊
		- 若deps 為空陣列，就會被系統認定不會被改變的依賴項目，回傳的函式物件就會以記憶體內的目前最新函式物件回傳，而不重新以baseFunction為主來從而建立新函式物件
		- 若沒添加\[deps\]，就會被系統認定為一直被改變的依賴項目，進而每一次執行都會重新以baseFunction為主來建立新的函式物件回傳
		- 若添加\[a, b\]，會先判斷a或者b是否有任一變動，有變動才重新以baseFunction為主來建立新的函式物件回傳；沒變動就不執行，直接回傳記憶體內的目前最新函式物件
```
const callbackResult = useCallback(baseFunction, [a, b])
```





### useCallback 何時檢查並觸發？
[[@vencovskyAnswerWhenUse2019]]

> useCallback
> On every render, everything that's inside a functional component will run again.

重點：
- 每一次執行元件的render函式就會執行useCallback，並檢查useCallback所依賴的內容是否有變動。

### function 被儲存在哪？

基本上會儲存在React 體系下內部定義的儲存區塊


## 複習


#🧠 React useCallback 在元件上來說是什麼？(別說用途)  ->->-> `useCallback本身是一個內建Hook，註冊在元件上`
<!--SR:!2024-04-23,280,230-->

#🧠 React useCallback 的用途為何 ->->-> `最主要是會依據依賴項目是否變動來決定是否重建函式物件並儲存在記憶體中，若變動就建立新函式物件和新closure，接著儲存並回傳，若沒變動就以目前記憶體的最新函式物件來回傳`
<!--SR:!2024-10-06,446,250-->

#🧠 React useCallback 主要解決了什麼問題？ ->->-> `解決memo本身的重建問題`
<!--SR:!2024-08-05,405,250-->

#🧠 React useCallback 主要解決了React.memo本身的重建問題，具體是什麼？ ->->-> `每一次渲染函式被呼叫就重建物件(函式物件)，將這些物件搭載至特定元件A的props，會因為物件在reference value上會是不一樣而導致元件A的props比對結果都不一樣，進而無法正常使用memo`
<!--SR:!2024-09-24,434,250-->

#🧠 useCallback在React的命名緣由為何？ ->->-> `useCallback 如同名稱那樣，會專門建立並儲存一個特定function來作為特定情況下要使用的函式`
<!--SR:!2023-11-11,242,250-->

#🧠 React useCallback 何時檢查並觸發？->->-> `每一次執行元件的render函式就會執行useCallback，並檢查useCallback所依賴的內容是否有變動。`
<!--SR:!2024-09-28,441,250-->


#🧠 React useCallback 所建立的函式都會儲存在記憶體的哪邊？ ->->-> `基本上會儲存在React 體系下內部定義的儲存區塊`
<!--SR:!2024-09-18,431,250-->

#🧠 React useCallback 語法會是什麼？ ->->-> `useCallback(baseFunction, [deps])`
<!--SR:!2023-08-04,189,250-->

#🧠 React useCallback 語法會是useCallback(baseFunction, \[deps\])中的baseFunction 是什麼？用途是什麼？ ->->-> `是用函式物件來定義每一次所建立的函式物件之基本函式架構-baseFunction`
<!--SR:!2023-12-10,101,230-->

#🧠 React useCallback 語法會是useCallback(baseFunction, \[deps\])中的\[deps\] 是什麼？用途是什麼？->->-> `依賴項目所構成的陣列，決定是否要在基本函式架構baseFunction搭配目前的依賴項目來建立新的函式物件，其函式物件會擁有新的closure`
<!--SR:!2024-04-04,329,250-->


#🧠 useCallback(baseFunction, \[deps\]) 會回傳什麼？(請盡量說到closure) ->->-> `根據[deps]來決定回傳新函式物件或者記憶體儲存的函式物件，其函式物件會夾帶closure，該closure的識別字會是特定執行時機下的記憶體區塊`
<!--SR:!2024-08-21,415,250-->


#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是空陣列，就表示什麼？ ->->-> `就會被系統認定不會被改變的依賴項目`
<!--SR:!2023-08-01,187,250-->
#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是空陣列，其useCallback回傳什麼？ ->->-> `回傳的函式物件就會以記憶體內的目前最新函式物件回傳，而不重新以baseFunction為主來從而建立新函式物件`
<!--SR:!2023-08-08,192,250-->

#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是空陣列，其useCallback會重新建立函式物件嗎 ->->-> `並不會`
<!--SR:!2025-01-27,519,250-->

#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是沒填的話，就表示什麼？ ->->-> `就會被系統認定為一直被改變的依賴項目`
<!--SR:!2024-12-18,489,250-->

#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是沒填的話，其useCallback回傳什麼？->->-> `進而每一次執行都會重新以baseFunction為主來建立新的函式物件回傳`
<!--SR:!2023-08-10,193,250-->

#🧠 useCallback(baseFunction, \[deps\]) 中的第二參數是填入\[a, b\]，就表示什麼？ ->->-> `會先判斷a或者b是否有任一變動，有變動才重新以baseFunction為主來建立新的函式物件回傳；沒變動就不執行，直接回傳記憶體內的目前最新函式物件`
<!--SR:!2024-09-27,440,250-->






---
Status: #🌱 #📝
Tags:
[[React]]
Links:
[[React.memo 比對方式會採用於JS的currProp === prevProp 而衍生出props對應著物件的元件a會因為渲染函式一直邊呼叫邊重建物件而無法讓元件a能夠正常使用memo]]

References:
[[@reactHooksAPICanKao]]
[[@ithomeDay9ReactHookPianRenShi]]