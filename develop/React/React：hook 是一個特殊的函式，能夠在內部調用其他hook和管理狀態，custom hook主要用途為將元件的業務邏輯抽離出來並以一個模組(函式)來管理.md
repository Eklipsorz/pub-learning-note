## 描述




### hook 

1. hook 本身是函式，其名稱會是以use開頭
2. 該函式可以調用其他hook(含custom hook)以及管理狀態

定義是：
- 一般函式
- 呼叫hook和管理狀態？

### custom hook 用途為

> functions which can contain stateful logic
>- outsource stateful logic into re-usable functions

>unlike regular function, custom hooks can use other react hooks and react state

> with custom hooks, you can outsource logic, which you might be using in different components into a custom hook, which you can the call from all these various component

- 將元件的業務邏輯抽離出來並以一個模組(函式)來管理：主要將元件上的狀態上業務邏輯外包(outsource)給hook來做，並且將hook打造成可重復性呼叫的function，以便讓其他元件也能使用該hook


### outsource 命名緣由

outsource：
> If a company outsources, it pays to have part of its work done by another company.

重點：
- outsource 是指將原本自己負責的任務內容分給其他人來做

## 複習

#🧠 React：hook 本質上是什麼？ ->->-> ` hook 本身是函式`
<!--SR:!2023-08-24,194,250-->

#🧠 React：hook 名稱會有什麼特徵 ->->-> `開頭都會有use開頭`
<!--SR:!2024-03-08,237,230-->

#🧠 React：hook 跟一般函式差別是什麼？ ->->-> `hook 可以調用其他hook(含custom hook)以及管理狀態`
<!--SR:!2023-12-15,102,230-->

#🧠  React： hook 可以調用其他hook以及管理狀態，其中調用其他hook包含了哪些hook？->->-> `內建hook和自製hook`
<!--SR:!2024-05-24,311,230-->

#🧠 outsource 命名緣由為何？ ->->-> `本身是指將原本自己負責的任務內容分給其他人來做`
<!--SR:!2023-08-23,193,250-->

#🧠 React：custom hook 的用途是什麼？->->-> `將元件的業務邏輯抽離出來並以一個模組(函式)來管理`
<!--SR:!2023-08-21,191,250-->

#🧠 React：custom hook 的用途是將元件的業務邏輯抽離出來並以一個模組(函式)來管理，那麼custom hook可以供給其他component使用嗎 ->->-> `可以`
<!--SR:!2025-01-07,491,250-->



#🧠 React：custom hook 主要負責哪種業務邏輯？ ->->-> `狀態、effect`
<!--SR:!2023-09-05,197,249-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: