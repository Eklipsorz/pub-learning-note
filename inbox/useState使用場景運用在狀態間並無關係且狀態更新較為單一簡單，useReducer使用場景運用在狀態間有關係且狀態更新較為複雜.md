## 描述


### useState 使用場景

> useState ：
> - your main state management tool
> - great for independent pieces of state/data
> - great if state updates are easy and limited to a few kinds of updates

重點：
- 盡量將useState作為主要狀態管理工具
- useState 適合 **多個狀態且狀態都毫無相關**
- useState 適合 **狀態更新方式是簡單且每個狀態只受限於各自獨有的狀態更新函式來進行**

### useReducer 使用場景

> useReducer：
> - great if you need "more power"
> - should be considered if you have related pieces of state/data
> - can be helpful if you have more complex state updates

> do not always useReducer because often that will be overkill
> if you have just a simple state that just switches between two different value for example

重點：
- useReducer 適合以object作為狀態的場景
- useReducer 適合多個狀態且狀態間都有關係/相互改變
- ~~useReducer 適合狀態更新很煩瑣和複雜~~
- useReducer 適合狀態更新上不只於各自獨有的狀態更新函式


### useState ＋ useReducer 具體可以合併使用

useReducer 使用上可允許：
1. 1~N個useReducer
2. 1~N個useReducer + 1~N個useState

## 複習

#🧠 在通常情況下，預設使用哪一種React體系的狀態管理工具 ->->-> `useState`
<!--SR:!2022-09-23,3,250-->

#🧠 React 的 useState 使用場景 是什麼？ ->->-> `適用於多個狀態且狀態間都毫無相關、狀態更新本身只受限於各自獨有的狀態更新函式`


#🧠 React 的 useReducer 使用場景 是什麼？ ->->-> `適合多個狀態且狀態間都有關係/相互改變、狀態更新上不只於各自獨有的狀態更新函式`

#🧠 React 的 useState能和useReducer一同在同一個元件使用嗎？具體會是哪一種形式 ->->-> `可以，1. 1~N個useReducer 2. 1~N個useReducer + 1~N個useState`

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React： 針對useReducer 所擁有的大狀態下的一小部分狀態來作為useEffect的depenedency，並且它們只要變動的話，就會在updating階段觸發時檢查到dependency變動而執行callback]]
[[React：使用useState 來管理多個狀態的潛在問題會容易衍生難以控管、維護狀態且bug眾多的代碼]]
References: