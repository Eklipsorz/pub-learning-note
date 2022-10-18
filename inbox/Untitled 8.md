## 描述


hook ：

- 名稱皆為use開頭

- 本身是一般的函式


### hook 

1. hook 本身是函式，其名稱會是以use開頭
2. 該函式與一般函式的最大差別就是可以調用



functions which can contain stateful logic

- outsource stateful logic into re-usable functions

將狀態處理相關的邏輯弄入可重複使用的函式裡頭

  

unlike regular function, custom hooks can use other react hooks and react state

->

hook function 可調用其他react hook(包含custom hook)的內容和狀態

  

with custom hooks, you can outsource logic, which you might be using in different components into a custom hook, which you can the call from all these various component

-> 有了custom hook，可以元件上的業務邏輯外包給一個hook來實現，並於其他component呼叫該hook

  

so it is simply a mechanism of reusing logic,

  

outsource：

If a company outsources, it pays to have part of its work done by another company.

## 複習


---
Status: 
Tags:
Links:
References: