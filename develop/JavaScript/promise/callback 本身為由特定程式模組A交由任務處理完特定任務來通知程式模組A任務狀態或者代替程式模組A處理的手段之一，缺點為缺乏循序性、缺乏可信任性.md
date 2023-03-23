## 描述


callback 本身為由特定程式模組A交由特定任務處理完特定任務來通知程式模組A任務狀態或者代替程式模組A處理的手段之一

本身在任意任務執行上具有兩大缺點：
- 使用callback來搭配任務執行會缺乏循序性
- 缺乏可信任性


### 缺乏循序性

1. 使用callback來搭配任務會缺乏循序性，或者說執行其程式碼的執行順序並不保證按照位置順序來執行
2. 若強迫每個callback為主的程式碼按照預期順序來執行，容易提升開發/維護難度

人類思考總是以
1. 循序、多個任務切換的角度來規劃每一件事情
2. 對於缺乏循序性會違背人類思考，容易使開發者誤會callback的執行順序


#### 案例
假如doA至doF皆為非同步任務
```
doA(function () {
	doB();

	doC(function() {
		doD();
	})

	doE();
})

doF();
```
執行順序會是：
```
doA();
doF();
doB();
doC();
doE();
doD();
```

若doA和doC為同步任務，而非同步任務的話，執行順序會是：
```
doA();
doB();
doC();
doD();
doE();
doF();
```

### 缺乏可信任性

1. 無法確保callback轉交給任務後，它會如何執行？
	- 任務可以重複執行callback好幾次
	- 任務可以選擇不執行callback
	- 任務執行callback的時機點過早或者過晚

[[@OopWhatInversion]]
> The Inversion-of-Control (IoC) pattern, is about providing any kind of callback (which controls reaction), instead of acting ourself directly (in other words, inversion and/or redirecting control to external handler/controller)



總結為：
- inversion of control：呼叫端所定義的程式碼-callback本身是由呼叫端構成，所以預期會是由呼叫端本身決定何時執行，但在將callback給予特定任務來處理時，會將callback轉由任務執行，這等同於變相地，由程式碼/第三方程式碼來決定呼叫端所定義的程式碼何時執行。
- 細節：
	- callback會是呼叫端的一部分
	- 當哪個程式碼決定callback的執行，就是由該程式碼決定呼叫端的程式碼執行



#### 案例

假如公司要求購買每一項東西時，都要呼叫追蹤交易的第三方服務，然後指定callback來由它負責付款和顯示付款成功的畫面。

然而callback的執行控制權會轉由第三方服務來執行，由它決定callback要執行幾次、執行時機、是否要執行。
```
// 追蹤交易來統計的第三方服務
analytics.trackPurchase(handler);
function handler() {
	chargeCreditCard();
	displayThankyouPage();
}
```


## 複習

#🧠 callback 在任務上做什麼？ ->->-> `callback 本身為由特定程式模組A交由任務處理完特定任務來通知程式模組A任務狀態或者代替程式模組A處理的手段之一`
<!--SR:!2023-06-15,91,250-->

#🧠 callback 在任意任務執行的實現上具有兩大缺點，請問是哪兩大？->->-> `- 使用callback來搭配任務會缺乏循序性 - 缺乏可信任性`
<!--SR:!2023-03-29,41,230-->

#🧠 callback 在任務執行的實現上具有兩大缺點，缺乏循序性是其中之一，請說明為何 ->->-> `由於人類思考總是以循序、多個任務切換的角度來規劃每一件事情、而使用callback來搭配任務執行會缺乏循序性，或者說執行其程式碼的執行順序並不保證按照位置順序來執行，所以 對於缺乏循序性會違背人類思考，容易使開發者誤會callback的執行順序`
<!--SR:!2023-05-25,72,229-->

#🧠 callback 在任務執行的實現上具有兩大缺點，缺乏循序性是其中之一，若強迫若強迫每個callback為主的程式碼按照順序來執行，可以嗎？為什麼？  ->->-> `若強迫每個callback為主的程式碼按照預期順序來執行，容易提升開發/維護難度`
<!--SR:!2023-05-19,73,250-->

#🧠 callback 在任務執行的實現上具有兩大缺點， 缺乏可信任性是其中之一，請說明為何 ->->-> ` 無法確保callback轉交給任務後，它會如何執行？比如- 任務可以重複執行callback好幾次- 任務可以選擇不執行callback- 任務執行callback的時機點過早或者過晚`
<!--SR:!2023-06-02,80,250-->

#🧠 callback 在任務執行的實現上具有兩大缺點， 缺乏可信任性是其中之一，而這歸咎於Inversion of control，請問它是什麼？->->-> `任何種類的callback之執行控制權從程式模組A反轉成不是由程式模組A來控制執行，而是轉由其他外部程式模組。在這裡會是指被接收callback的非同部任務來決定`
<!--SR:!2023-06-03,81,250-->

#🧠 若假如doA至doF皆為非同步任務，那麼各個函式的執行順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-1_phwg4u.png) ->->-> `doA() -> doF() -> doB() -> doC() -> doE() ->doD()`
<!--SR:!2023-05-06,64,250-->


#🧠 若除了doA和doC為同步任務，剩下就皆為非同步任務，那麼各個函式的執行順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-1_phwg4u.png) ->->-> `doA() -> doB() -> doC() -> doD() -> doE() -> doF()`
<!--SR:!2023-05-24,78,250-->


#🧠 假如公司要求購買每一項東西時，都要呼叫追蹤交易的第三方服務，然後指定callback來由它負責付款和顯示付款成功的畫面，請問這會有啥潛在問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-2_lrqyyv.png) ->->-> `難以信任第三方服務會正常執行callback，callback的執行控制權會轉由第三方服務來執行，由它決定callback要執行幾次、執行時機、是否要執行。`
<!--SR:!2023-05-11,68,250-->

#🧠 callback 會有 inversion of control 嗎？仔細說明，以呼叫端、callback、特定任務來舉例 ->->-> `inversion of control：呼叫端所定義的程式碼-callback本身是由呼叫端構成，所以預期會是由呼叫端本身決定何時執行，但在將callback給予特定任務來處理時，會將callback轉由任務執行，這等同於變相地，由程式碼/第三方程式碼來決定呼叫端所定義的程式碼何時執行。`
<!--SR:!2023-03-28,5,248-->

#🧠 callback 會呈現出 inversion of control ，那麼callback和呼叫端之間的關係是如何 以及誰執行callback又是代表著 ->->-> `- callback會是呼叫端的一部分- 當哪個程式碼決定callback的執行，就是由該程式碼決定呼叫端的程式碼執行`
<!--SR:!2023-03-28,5,248-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@OopWhatInversion]]