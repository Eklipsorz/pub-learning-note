## 描述


### useState 使用場景

> useState ：
> - your main state management tool
> - great for independent pieces of state/data
> - great if state updates are easy and limited to a few kinds of updates

重點：
- 盡量將useState作為主要狀態管理工具
- useState 適合 **多個狀態且狀態都毫無相關**
- useState 適合 **狀態更新方式是簡單且受限於幾個固定途徑來進行**

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
- useReducer 的狀態更新很煩瑣和複雜


### useState ＋ useReducer 具體可以合併使用

useReducer 使用上可允許：
1. 1~N個useReducer
2. 1~N個useReducer + 1~N個useState

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References: