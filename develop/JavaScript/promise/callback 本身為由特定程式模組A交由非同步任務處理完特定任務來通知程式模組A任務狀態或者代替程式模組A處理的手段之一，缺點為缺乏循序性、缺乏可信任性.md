## 描述


callback 本身為由特定程式模組A交由非同步任務處理完特定任務來通知程式模組A任務狀態或者代替程式模組A處理的手段之一

本身在非同步任務上具有兩大缺點：
- 使用callback來搭配非同步任務會缺乏循序性
- 缺乏可信任性


### 缺乏循序性

1. 使用callback來搭配非同步任務會缺乏循序性，或者說執行其程式碼的執行順序並不保證按照位置順序來執行
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

1. 無法確保callback轉交給非同步任務後，它會如何執行？
	- 非同步任務可以重複執行callback好幾次
	- 非同步任務可以選擇不執行callback
	- 非同步任務執行callback的時機點過早或者過晚

[[@OopWhatInversion]]
> The Inversion-of-Control (IoC) pattern, is about providing any kind of callback (which controls reaction), instead of acting ourself directly (in other words, inversion and/or redirecting control to external handler/controller)



總結為：
- inversion of control：任何種類的callback之執行控制權從程式模組A反轉成不是由程式模組A來控制執行，而是轉由其他外部程式模組。在這裡會是指被接收callback的非同部任務來決定


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

#🧠 callback 在非同步任務上做什麼？ ->->-> `callback 本身為由特定程式模組A交由非同步任務處理完特定任務來通知程式模組A任務狀態或者代替程式模組A處理的手段之一`
<!--SR:!2023-02-04,10,250-->

#🧠 callback 在非同步任務的實現上具有兩大缺點，請問是哪兩大？->->-> `- 使用callback來搭配非同步任務會缺乏循序性 - 缺乏可信任性`
<!--SR:!2023-01-31,6,230-->

#🧠 callback 在非同步任務的實現上具有兩大缺點，缺乏循序性是其中之一，請說明為何 ->->-> `由於人類思考總是以循序、多個任務切換的角度來規劃每一件事情、而使用callback來搭配非同步任務會缺乏循序性，或者說執行其程式碼的執行順序並不保證按照位置順序來執行，所以 對於缺乏循序性會違背人類思考，容易使開發者誤會callback的執行順序`
<!--SR:!2023-02-11,12,229-->

#🧠 callback 在非同步任務的實現上具有兩大缺點，缺乏循序性是其中之一，若強迫若強迫每個callback為主的程式碼按照順序來執行，可以嗎？為什麼？  ->->-> `若強迫每個callback為主的程式碼按照預期順序來執行，容易提升開發/維護難度`
<!--SR:!2023-02-04,10,250-->

#🧠 callback 在非同步任務的實現上具有兩大缺點， 缺乏可信任性是其中之一，請說明為何 ->->-> ` 無法確保callback轉交給非同步任務後，它會如何執行？比如- 非同步任務可以重複執行callback好幾次- 非同步任務可以選擇不執行callback- 非同步任務執行callback的時機點過早或者過晚`
<!--SR:!2023-02-04,10,250-->

#🧠 callback 在非同步任務的實現上具有兩大缺點， 缺乏可信任性是其中之一，而這歸咎於Inversion of control，請問它是什麼？->->-> `任何種類的callback之執行控制權從程式模組A反轉成不是由程式模組A來控制執行，而是轉由其他外部程式模組。在這裡會是指被接收callback的非同部任務來決定`
<!--SR:!2023-02-04,10,250-->

#🧠 若假如doA至doF皆為非同步任務，那麼各個函式的執行順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-1_phwg4u.png) ->->-> `doA() -> doF() -> doB() -> doC() -> doE() ->doD()`
<!--SR:!2023-02-04,10,250-->


#🧠 若除了doA和doC為同步任務，剩下就皆為非同步任務，那麼各個函式的執行順序為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-1_phwg4u.png) ->->-> `doA() -> doB() -> doC() -> doD() -> doE() -> doF()`
<!--SR:!2023-02-04,10,250-->


#🧠 假如公司要求購買每一項東西時，都要呼叫追蹤交易的第三方服務，然後指定callback來由它負責付款和顯示付款成功的畫面，請問這會有啥潛在問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674351614/blog/promise/callback/callback-problem-2_lrqyyv.png) ->->-> `難以信任第三方服務會正常執行callback，callback的執行控制權會轉由第三方服務來執行，由它決定callback要執行幾次、執行時機、是否要執行。`
<!--SR:!2023-02-04,10,250-->



---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@OopWhatInversion]]