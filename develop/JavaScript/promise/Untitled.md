## 描述

callback 本身為由特定程式模組A交由非同步任務處理完特定任務來通知程式模組A任務狀態或者代替程式模組A處理的手段之一

本身具有兩大缺點：
- 多callback間缺乏循序性
- 缺乏可信任性


### 缺乏循序性

1. callback 本身很難確保每一個callback都是循序執行，或者說執行callback的執行順序並不能確定按照位置順序來執行
2. 若強迫每個callback按照預期順序來執行，容易提升開發/維護難度

人類思考總是以
1. 循序、多個任務切換的角度來規劃每一件事情
2. 對於缺乏循序性會違背人類思考，容易使開發者誤會callback的執行順序


### 缺乏可信任性

1. 無法確保callback轉交給非同步任務後，它會如何執行？
	- 非同步任務可以重複執行callback好幾次
	- 非同步任務可以選擇不執行callback
	- 非同步任務執行callback的時機點過早或者過晚

[[@OopWhatInversion]]
> The Inversion-of-Control (IoC) pattern, is about providing any kind of callback (which controls reaction), instead of acting ourself directly (in other words, inversion and/or redirecting control to external handler/controller)



總結為：
- inversion of control：任何種類的callback之執行


#### 案例

假如公司要求購買每一項東西時，都要呼叫追蹤交易的第三方服務，然後指定callback來由它負責付款和顯示付款成功的畫面。

然而第三方服務這時就
```
// 追蹤交易來統計的第三方服務
analytics.trackPurchase(handler);
function handler() {
	chargeCreditCard();
	displayThankyouPage();
}
```


## 複習


---
Status: #🌱 
Tags:
Links:
References:
[[@OopWhatInversion]]