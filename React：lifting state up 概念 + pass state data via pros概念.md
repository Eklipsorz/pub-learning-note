## 描述
[[@fooishReactTiShengGongYongZhuangTaiLifting]]
> 很常你會遇到一種情況是，有好幾個獨立元件同時都跟某個資料狀態 (shared state) 的改變有相依性，React 建議的處理模式是，將這個資料狀態提升 (lifting state up) 到這些元件的某個共同父元件 (closest common ancestor) 上面。

> 實作概念是，當子元件事件 (Child Events) 發生時，透過父元件傳進來的 callback function 通知父元件有資料變動，然後由父元件統一計算得到新的父元件 state，然後透過 props 反應資料更新回這些子元件。

[[@freecodecampWhatLiftingState2021]]
> This is where the concept of lifting state up comes in.

> We lift up state to a common ancestor of components that need it, so that they can all share in the state. This allows us to more easily share state among all of these components that need rely upon it.





重點：
- 在元件間AB本身若沒有parent-child關係的情況下，元件AB不能夠直接互相傳遞資訊至對方元件，目前只允許props概念-由parent元件往child元件傳遞
- lifting state up 概念： 將特定元件A的狀態、更新用狀態函式往上(parent方向)找到parent 元件註冊自己元件A的狀態、更新用狀態。
- lift state up 概念 + pass state data via pros概念 來實現多個元件間共享狀態、從他們元件角度來渲染對方元件。
-  lift state up 概念 + pass state data via pros概念 具體是：
	- 若要讓元件AB共享彼此間的狀態並從他們的角度來渲染對方元件，則必須要讓元件AB所擁有的狀態往上提升至他們所共有的parent元件，並且在從parent元件那使用props概念來往下分享給元件AB他們彼此間的狀態
	- 換言之，就在parent元件上註冊元件AB所擁有的狀態、對應狀態更新函式，然後藉由props概念接收狀態、函式給元件AB

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
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
[[@freecodecampWhatLiftingState2021]]
[[@fooishReactTiShengGongYongZhuangTaiLifting]]