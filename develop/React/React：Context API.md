## 描述
React Context
1. 元件間的內建狀態儲存器
2. 在不依賴額外的props chain的情況下，實現元件間彼此交換狀態和觸發渲染
3. 在不依賴額外的props chain的情況下，元件之間的狀態、更新狀態用函式可以直接透過Context面對面交換。


1. component-wide "behind the scenes", state storage, built into React

2. and this then allows us to, for example, trigger a action in that component-wide State Storage, then directly pass that to the component

3. without build such a long prop chain


舉例：
- Login登入後，就會將狀態發送至state storage，然後再由state storage直接發送至shop元件
- 增加產品至購物車後，就將狀態發送至state storage，然後再由state storage直接發送至cart元件
- 從中不再依賴著props所建立的chain


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663607881/blog/react/context/component-wide-state-storage_caeat2.png)




### xxxx-wide 命名緣由

> -wide combines with nouns to form adjectives which indicate that something exists or happens throughout the place or area that the noun refers to. 

重點：

- xxx-wide ：-wide會與名詞來形成一個形容詞來表示特定事物存在於/特定事物發生在xxx所指的區域 或者指的是 xxx所指的區域之範圍內

- component-wide：元件範圍內



context => 定義如何執行的資訊

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：使用如Redux或者Context這種集中狀態機制是為了讓多個元件下能夠彼此共享狀態和彼此觸發渲染週期]]
[[React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染]]
References: