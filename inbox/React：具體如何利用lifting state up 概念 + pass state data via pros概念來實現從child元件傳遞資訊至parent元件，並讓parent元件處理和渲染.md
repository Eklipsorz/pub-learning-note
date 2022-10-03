## 描述
[[@fooishReactTiShengGongYongZhuangTaiLifting]]
> 很常你會遇到一種情況是，有好幾個獨立元件同時都跟某個資料狀態 (shared state) 的改變有相依性，React 建議的處理模式是，將這個資料狀態提升 (lifting state up) 到這些元件的某個共同父元件 (closest common ancestor) 上面。

> 實作概念是，當子元件事件 (Child Events) 發生時，透過父元件傳進來的 callback function 通知父元件有資料變動，然後由父元件統一計算得到新的父元件 state，然後透過 props 反應資料更新回這些子元件。




重點：
- lifting state up 概念： 將特定元件A的狀態往上傳遞至parent元件上，好讓parent元件接收並處理
- lifting state up 實現：將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動
- lifting state up 概念 + pass state data via props 概念： 將特定元件A的狀態往上傳遞至parent元件上，並讓parent元件接收到狀態來修改渲染用的資料，接著觸發渲染透過props往下將新資訊更新至子元件來重新渲染
-  lift state up 概念 + pass state data via props 實現：將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動，接著透過執行parent元件上的setState來依據資料更新以及觸發渲染，觸發後會透過props將新狀態往下傳遞來構築新的child元件和parent

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661350629/blog/react/state/lifting-state-up_props_be8lkl.png)


### 特定元件A的狀態改註冊至其parent元件上，算是lifting state up的技術一部分嗎？

 為什麼？ `並不算，其原因為lifting state up概念上是指將目前元件上的狀態往上傳遞至其parent元件，讓parent元件接收到並處理，而非註冊在parent元件`

#### 總結差異：

##### 狀態所有權
1. 特定元件A的狀態註冊在其parent元件上 vs lifting state up ：
	- 前者中，特定元件A由於轉移狀態，所以沒有被轉移過的狀態，而parent元件擁有特定元件A的狀態
	- 後者中，特定元件A和parent元件的狀態還保有原有樣子

##### 傳遞狀態方向
1. lifting state up純粹將目前元件上的狀態往上傳遞至其parent元件，讓parent元件接收到並處理
2. 特定元件A的狀態註冊在其parent元件：轉移後，parent元件就把狀態往下傳遞特定元件A


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
<!--SR:!2022-10-04,28,250-->


#🧠 React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染? 具體實現是如何？ ->->-> `將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動，接著透過執行parent元件上的setState來依據資料更新以及觸發渲染，觸發後會透過props將新狀態往下傳遞來構築新的child元件和parent`
<!--SR:!2022-11-29,60,250-->


#🧠 React： lifting state up 概念是什麼？(請說到傳遞和接收者要做啥) ->->-> `將特定元件A的狀態往上傳遞至parent元件上，好讓parent元件接收並處理`
<!--SR:!2022-10-31,28,250-->


#🧠 React： lifting state up 概念是什麼？ ->->-> `將特定元件A的狀態往上傳遞至parent元件上，好讓parent元件接收並處理`
<!--SR:!2022-10-03,10,250-->


#🧠 React： lifting state up 概念的實作會是什麼？->->-> `將特定元件A的狀態藉由parent元件給予的callback來通知parent元件有資料變動`
<!--SR:!2022-10-31,28,250-->


#🧠 React：特定元件A的狀態註冊在其parent元件上，特定元件A和parent元件的狀態所有權分別如何？ ->->-> `特定元件A由於轉移狀態，所以沒有被轉移過的狀態，而parent元件擁有特定元件A的狀態`
<!--SR:!2022-10-31,28,250-->

#🧠 React：特定元件A利用lifting state up方式傳遞自己狀態至其parent元件上，特定元件A和parent元件的狀態所有權分別如何？ ->->-> `特定元件A和parent元件的狀態還保有原有樣子`
<!--SR:!2022-10-31,28,250-->

#🧠 React：lifting state up vs.  特定元件A的狀態改註冊至其parent元件 差異是什麼？(簡答)->->-> `差異：狀態所有權、傳遞狀態方向`
<!--SR:!2022-10-31,28,250-->

#🧠 React：特定元件A利用lifting state up方式傳遞自己狀態至其parent元件上，特定元件A和parent元件的傳遞狀態方向是？ ->->-> `lifting state up純粹將目前元件上的狀態往上傳遞至其parent元件，讓parent元件接收到並處理`
<!--SR:!2022-10-27,24,250-->

#🧠 React：特定元件A的狀態註冊在其parent元件上，特定元件A和parent元件的傳遞狀態方向是？ ->->-> `特定元件A的狀態註冊在其parent元件：轉移後，parent元件就把狀態往下傳遞特定元件A`
<!--SR:!2022-10-31,28,250-->

#🧠 React：若特定元件A的狀態改註冊至其parent元件上，算是lifting state up的技術一部分嗎？ 為什麼？請試著以註冊的角度來開始說起->->-> `並不算，本質上就不一樣，註冊後，狀態會被轉移至parent元件，並由parent元件傳遞資訊至特定元件A；而lifting state up則是在保留狀態下，往上傳遞自己狀態至parent元件`
<!--SR:!2022-10-31,28,250-->




---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：具體如何利用lifting state up 概念 + pass state data via pros概念來實現從child元件傳遞資訊至parent元件，並讓parent元件處理和渲染]]
References:
[[@freecodecampWhatLiftingState2021]]
[[@fooishReactTiShengGongYongZhuangTaiLifting]]