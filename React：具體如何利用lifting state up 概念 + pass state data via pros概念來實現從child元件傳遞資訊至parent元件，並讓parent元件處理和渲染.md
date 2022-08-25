## 描述
[[@fooishReactTiShengGongYongZhuangTaiLifting]]
> 很常你會遇到一種情況是，有好幾個獨立元件同時都跟某個資料狀態 (shared state) 的改變有相依性，React 建議的處理模式是，將這個資料狀態提升 (lifting state up) 到這些元件的某個共同父元件 (closest common ancestor) 上面。

> 實作概念是，當子元件事件 (Child Events) 發生時，透過父元件傳進來的 callback function 通知父元件有資料變動，然後由父元件統一計算得到新的父元件 state，然後透過 props 反應資料更新回這些子元件。




重點：
- lifting state up 概念： 將特定元件A的狀態往上傳遞至parent元件上
- lifting state up 實現：將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動
- lifting state up 概念 + pass state data via props 概念： 將特定元件A的狀態往上傳遞至parent元件上，並讓parent元件接收到狀態來修改渲染用的資料，接著觸發渲染透過props往下將新資訊更新至子元件來重新渲染
-  lift state up 概念 + pass state data via props 實現：將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動，接著透過執行parent元件上的setState來依據資料更新以及觸發渲染，觸發後會透過props將新狀態往下傳遞來構築新的child元件和parent

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661350629/blog/react/state/lifting-state-up_props_be8lkl.png)

### 解析

because we can now store our state in that closest involved component.

So in that parent component which has access to both involved components by lifting our state up.


> The app component in our application has access to both the new expense and the expenses component because it renders both components in its returned JSX code, that's why we wanna utilize that

```
<NewExpense />
<Expenses />
```


這裡指的是app component能夠存取其child元件下面的資訊(props夾帶的資訊)

## 複習
#🧠 React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染? 概念上要如何解決 ->->-> `	 將特定元件A的狀態往上傳遞至parent元件上，並讓parent元件接收到狀態來修改渲染用的資料，接著觸發渲染透過props往下將新資訊更新至子元件來重新渲染`
<!--SR:!2022-08-27,3,250-->


#🧠 React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染? 具體實現是如何？ ->->-> `將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動，接著透過執行parent元件上的setState來依據資料更新以及觸發渲染，觸發後會透過props將新狀態往下傳遞來構築新的child元件和parent`
<!--SR:!2022-08-27,3,250-->


#🧠 React： lifting state up 概念是什麼？ ->->-> `將特定元件A的狀態往上傳遞至parent元件上`
<!--SR:!2022-08-27,3,250-->

#🧠 React： lifting state up 概念是什麼？->->-> `將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動`
<!--SR:!2022-08-27,2,230-->


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染]]
References:
[[@freecodecampWhatLiftingState2021]]
[[@fooishReactTiShengGongYongZhuangTaiLifting]]