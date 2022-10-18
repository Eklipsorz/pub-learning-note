## 描述

[[@ithomeDay06ShengMingYouXianHaoHaoBaWoLifecycle]]
> ### componentDidUpdate(prevProps, prevState, snapshot)

> 再次完成render後會執行`componentDidUpdate`，在此貼心的react會傳給你更新前的props(`prevProps`)、更新前的state(`prevState`)


重點：
- componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼
- componentDidUpdate 源自於class-based component的函式
- 語法為
	- prevProps ：更新前的props資訊
	- preState：更新前的state 資訊
```
componentDidUpdate(prevProps, prevState, snapshot)
```

## 複習

#🧠 React：componentDidUpdate 是源自於哪個元件開發的函式 ->->-> `class-based component`
<!--SR:!2022-10-27,10,250-->

#🧠 React：componentDidUpdate 語法為何？ ->->-> `componentDidUpdate(prevProps, prevState) {.....}`
<!--SR:!2022-10-27,9,250-->

#🧠 React：componentDidUpdate 語法為componentDidUpdate(prevProps, prevState) {.....}，請問prevProps和preState是什麼？ ->->-> `	- prevProps ：更新前的props資訊 - preState：更新前的state 資訊`
<!--SR:!2022-10-26,9,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@ithomeDay06ShengMingYouXianHaoHaoBaWoLifecycle]]