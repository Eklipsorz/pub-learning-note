## 描述

[[@WhatPropDrilling2021]]
> **What is Prop Drilling?**

> Anyone who has worked in React would have faced this and if not then will face it definitely. Prop drilling is basically a situation when the same data is being sent at almost every level due to requirements in the final level. Here is a diagram to demonstrate it better. Data needed to be sent from _Parent_ to _ChildC._ In this article different ways to do that are discussed.


![](https://media.geeksforgeeks.org/wp-content/uploads/20210618101141/Untitled.png)



[[@HowAvoidProp2022]]
> **Prop drilling** is a situation where data is passed from one component through multiple interdependent components until you get to the component where the data is needed. Here's an illustration of prop drilling to help you understand:  

![](https://lh5.googleusercontent.com/K1veBT9r_aQPq_iYI9MdtljbsBu8egv7n8cu78fWqzL0POVn2xb66r_gEFgJ8qg9FxphsGFqNZIDQ3QZ0zuT-XtEcrpNVZylXvxhDTPAySL8_FJWiIGHlcXggcHYCFKaQeNp8HRQvCZZQHRULaf8_vtg8mgyZElVhkSiUYgicFQ0mo6zPgGve9-Pcg)

> Passing data through multiple components is not a good way of writing clean, reusable, and DRY code.






重點：
- prop drilling 概念為使用元件的props概念來對來源元件和目標元件之間的元件進行打洞的行為，該行為會使得資料從來源元件放入洞口就能直通到目標元件這進行相關渲染和處理。
- 具體為：來源元件會將資訊傳遞至元件1的attribute作為它的props，接著元件1轉遞資訊至下一個元件的attribute來作為它的props，最後轉遞資訊至目標元件作為其props來處理來源元件對於目標元件所想要達成的渲染畫面和服務。
![](https://media.geeksforgeeks.org/wp-content/uploads/20210618101141/Untitled.png)
- 通常使用在元件間的資料傳遞、狀態資料傳遞
- 缺點：
	- 





### 優缺點

[[@ithomeWantKnowReactb]]
> ### Props 的缺點

> Props 有一個特點，就是 props 不可跳層傳遞。

> 如果要將資料從上層 component 傳遞到較下層的 component 的話，則需要經過每一個中間層 component 的 props 才可送達目標的下層 component。

> 這種特性是 props 的優點。其資料流路徑明確，只要照著每一層 component 的 props 往上追朔即可找到資料源頭。然而當我們要把一個全域性的資料（e.g. UI 主題、時區、語系 ...etc）傳給許多下層 component 時，使用 props 就會變成一個噩夢。每一個中間層 component 都必須定義此 props 才能把資料送達目的地。這會導致幾個問題：

>-   污染中間層 component。不需要資料的中間層 component 也被迫定義對應的 props  
>-   當傳遞層數與傳遞的目標 component 過多時，會造成修改 props 與追朔資料流不易
    此時即使只是微小的修改，也需要修改眾多的中間層 component 才能達到目的。



[[@ReactzhuangtaiguanlishijianmantanPianyi]]
> • **优点：**显式优于隐式

> Prop Drilling 通过显式传递的方式，在一定程度上避免了过度使用全局变量造成的数据模型混乱。全局定义会导致变量难以追踪，因而当我们想要更新、删除某一个变量时，很难确定该变量是否正在被使用，莽撞的修改很可能造成预期之外的某个组件受到影响。

> • **缺点：**重构艰难
> 随着项目复杂度的增加，往往会出现某个prop的传递，穿透多个组件层级的应用场景，因而代码追溯长度也会不断增加，进而导致对component的性能分析异常困难，尤其是在进行代码重构时，积攒的负面影响便会爆发形成较大的阻碍。


重點：
- props drilling 優點：
	- 可透過減少全域環境或者共用資料儲存空間的使用機會來從而使全域環境或者共用資料儲存空間保持秩序，而非混亂
	- 與全域環境或者共用資料儲存空間的方法相比，元件獲取到的資料可以從drilling的方向得知該資料從何而來、哪個元件會改變到
- 缺點：
	- 無論單個元件架構為何，即使元件本身不適合使用props來接收，還是得滿足 **每個元件得必須提供props介面來接收** 這條件
	- 隨著專案規模發展，會使來源元件和目標元件之間的元件數過多，而這些元件都有機會透過props來修改要轉遞的資料，使得目標元件
### drill & drilling 命名緣由

drill
> to make a hole in something using a special tool
> to make a deep hole in the ground with a special machine in order to look for oil, gas, etc.:

重點：
- drill 使用特定工具對特定事物上製造深洞
- drilling 使用特定工具對特定事物上製造深洞的行為或者過程


## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@WhatPropDrilling2021]]
[[@HowAvoidProp2022]]
[[@ithomeWantKnowReactb]]