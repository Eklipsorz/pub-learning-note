## 描述




在Promise API時代前，callback交給任務A來執行所帶有的疑慮：
- 太早執行callback：當執行任務A時，callback是否就跟著任務A的執行而跟著執行？
- 太晚執行callback：若任務A是以非同步來執行callback，會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行。
- 呼叫callback的次數超過一次或者沒呼叫callback
- 沒有傳入任何必要的參數和環境給callback：若callback是以非同步任務來執行，其參數是否會以任務A的執行結果為主並加以處理？
- 因callback執行時拋出錯誤而產生預期外的結果，比如吞掉callback執行時拋出的錯誤或者例外，非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理、因系統接受到錯誤而採取預設的錯誤處理，而錯誤處理是以同步執行來執行，而callback是以非同步來執行，顯然會使callback整體變成Zalgo


在Promise 中分別針對這幾個問題來增強執行callback的被信任程度

### 太早執行callback

> 太早執行callback：當執行任務A時，callback是否就跟著任務A的執行而跟著執行？


在Promise中，callback只要放入Promise API下的then、catch、finally這些語法的話，就會以非同步來執行callback
```
Promise(...)
.then(callback);
```

另外即使Promise指定任務是立即會履行的任務，如以下，callback仍以非同步任務型式來被排程去執行。
```
new Promise((resolve, reject) => {
	resolve(10);
})
.then(callback);
```

### 太晚執行callback

> 太晚執行callback：若任務A是以非同步來執行callback，這會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行

在Promise中，非同步任務的排程會按照then、catch、finally的出現順序來決定，也就是可以藉由promise.then給定的API位置來由上至下按照位置順序去排程非同步任務callback，如下：Promise會製造fulfilled狀態或者rejected狀態的promise，並且呼叫其promise的then來讓callback1先執行，接著在執行callback2，最後在執行callback3
```
Promise(...)
.then(callback1, callback1)
.then(callback2, callback2)
.then(callback3, callback3)
```

### 呼叫callback的次數超過一次或者沒呼叫callback

> 呼叫callback的次數超過一次或者沒呼叫callback

callback適合的執行次數會是1次，而在Promise中，所有經由Promise.then所註冊的callback，只要該Promise被解析(resolve)或者被拒絕(rejected)，其對應的callback就只會因為Promise.then而被執行一次。

但不保證將相同callback註冊在多個Promise.then而產生出超過一次的callback之執行次數，然而執行次數的決定會是由註冊方來決定，而非交由原本無法信任的任務A來決定

### 沒有傳入任何必要的參數至callback

> 沒有傳入任何必要的參數和環境給callback：若callback是以非同步任務來執行，其參數是否會以任務A的執行結果為主並加以處理？

在Promise中，都會將fulfilled狀態或者rejected狀態的內容當作callback的參數來填入，所以只要設定fulfilled狀態或者rejected狀態的內容以及讓callback設定成合適形式的引數形式，就能確保callback能獲取到參數來執行。

其次可以利用函式本身的closure來記錄特定時期的記憶體區塊來進行處理


### 因callback執行時拋出錯誤而產生預期外的結果





> 因callback執行時拋出錯誤而產生預期外的結果，比如吞掉callback執行時拋出的錯誤或者例外，非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理、因系統接受到錯誤而採取預設的錯誤處理，而錯誤處理是以同步執行來執行，然而callback是以非同步來執行，顯然會使callback整體變成Zalgo


#### 未有對應錯誤處理來應對callback被執行時所拋出的錯誤


問題描述：
當包覆著對應callback的promise object被執行時，若拋出錯誤的話，promise 會自動將錯誤包裝成rejected狀態的promise來回傳，接著之後的錯誤處理很有可能會因為該object 未註冊著錯誤處理的callback而未能處理。


解法：
1. 註冊方只需要在後頭註冊負責錯誤處理的callback就能解決
2. 直接修改以最一開始的Promise object所擁有的狀態為rejected，進而讓它執行該Promise object原本的錯誤處理。


#### 因錯誤處理而使callback的執行方式會演變成Zalgo

問題描述：

預期情況下，還有衍生出Zalgo問題機會，比如由系統的內建錯誤處理攔截到錯誤，並且以同步形式來執行錯誤，然而在這裏的callback本身就受到Promise而以非同步執行，那麼會使整體的callback(含錯誤處理)在執行上變成難以區分其執行方式的Zalgo

解法：

1. 在Promise中，會將所有發生在callback上的錯誤和執行錯誤全以rejected狀態的promise來回傳給下一個Promise.then或者Promise.catch來接收，當他們接收到時，就會以非同步任務的形式來執行錯誤處理，確保另一個潛在的問題- 錯誤處理會不會致使callback的執行變成Zalgo


比如：當callback1執行時拋出錯誤時，這時系統會直接以fullfilled狀態的promise來呼叫它擁有的catch或者then來執行對應錯誤處理callback。
```
new Promise((resolve, reject) => {
	resolve(10);
})
.then(callback1)
.catch(callback2) // 或者 .then(callback1, callback1)
```




## 複習

#🧠 JavaScript：在Promise API時代前，callback交給任務A來執行所帶有的疑慮有哪些，主要講信任相關 ->->-> `太早執行callback、太晚執行callback、呼叫callback的次數超過一次或者沒呼叫callback、沒有傳入任何必要的參數和環境給callback、因callback執行時拋出錯誤而產生預期外的結果`
<!--SR:!2023-10-31,57,230-->

#🧠 JavaScript：在Promise API時代前，callback交給任務A來執行所帶有的疑慮有哪些，主要講信任相關，其中太早執行callback是指什麼？ ->->-> `當執行任務A時，callback是否就跟著任務A的執行而跟著執行？`
<!--SR:!2023-12-19,175,250-->

#🧠 JavaScript：在Promise API時代前，callback交給任務A來執行所帶有的疑慮有哪些，主要講信任相關，其中太晚執行callback是指什麼？->->-> `若任務A是以非同步來執行callback，會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行。`
<!--SR:!2024-01-09,189,250-->

#🧠 JavaScript：在Promise API時代前，callback交給任務A來執行所帶有的疑慮有哪些，主要講信任相關，其中沒有傳入任何必要的參數和環境給callback是指什麼？ ->->-> `若callback是以非同步任務來執行，其參數是否會以任務A的執行結果為主並加以處理？`
<!--SR:!2023-12-30,176,250-->

#🧠  JavaScript：在Promise API時代前，callback交給任務A來執行所帶有的疑慮有哪些，主要講信任相關，其中因callback執行時拋出錯誤會有什麼疑慮？->->-> `吞掉callback執行時拋出的錯誤或者例外，非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理、因系統接受到錯誤而採取預設的錯誤處理，而錯誤處理是以同步執行來執行，而callback是以非同步來執行，顯然會使callback整體變成Zalgo`
<!--SR:!2024-01-03,132,210-->


#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-太早執行callback?->->-> `在Promise中，callback只要放入Promise API下的then、catch、finally這些語法的話，就會以非同步來執行callback，另外即使Promise指定任務是立即會履行的任務，callback仍以非同步任務型式來被排程去執行。`
<!--SR:!2024-01-14,191,250-->

#🧠 `new Promise((resolve, reject) => { resolve(10); }).then(callback); ` 請問callback會以何種方式執行？ ->->-> ``
<!--SR:!2023-12-28,181,250-->


#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-太晚執行callback? ->->-> `在Promise中，非同步任務的排程會按照then、catch、finally的出現順序來決定，也就是可以藉由promise.then給定的API位置來由上至下按照位置順序去排程非同步任務callback`
<!--SR:!2023-12-02,163,250-->

#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-太晚執行callback? 請舉例來說，以三個callback 來說明 ->->-> ``
<!--SR:!2024-02-15,206,250-->

#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-呼叫callback的次數超過一次或者沒呼叫callback?  ->->-> `在Promise中，所有經由Promise.then所註冊的callback，只要該Promise被解析(resolve)或者被拒絕(rejected)，其對應的callback就只會因為Promise.then而被執行一次。`
<!--SR:!2024-01-17,194,250-->

#🧠 JavaScript：callback本身執行次數在理論上的執行次數會是多少？ ->->-> `1次`
<!--SR:!2024-02-18,209,250-->

#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-呼叫callback的次數超過一次或者沒呼叫callback? 但能夠完全保證嗎？ 其原因為何 ->->-> `不能，但不保證將相同callback註冊在多個Promise.then而產生出超過一次的callback之執行次數，然而執行次數的決定會是由註冊方來決定，而非交由原本無法信任的非同步任務A來決定`
<!--SR:!2023-12-05,166,250-->


#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-沒有傳入任何必要的參數至callback?  ->->-> `在Promise中，都會將fulfilled狀態或者rejected狀態的內容當作callback的參數來填入，所以只要設定fulfilled狀態或者rejected狀態的內容以及讓callback設定成合適形式的引數形式，就能確保callback能獲取到參數來執行。、其次可以利用函式本身的closure來記錄特定時期的記憶體區塊來進行處理`
<!--SR:!2023-12-25,178,250-->

#🧠 JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-因callback執行時拋出錯誤而產生預期外的結果，先以吞掉callback執行時拋出的錯誤或者例外，非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理來說 ->->-> `當包覆著對應callback的promise object被執行時，若拋出錯誤的話，promise 會自動將錯誤包裝成rejected狀態的promise來回傳， 註冊方只需要在後頭註冊負責錯誤處理的callback就能解決`
<!--SR:!2023-12-27,173,250-->


#🧠  JavaScript：在Promise API時代中，它是如何面對先前沒Promise時所會有的疑慮-因錯誤處理而使callback的執行方式會演變成Zalgo->->-> `在Promise中，會將所有發生在callback上的錯誤和執行錯誤全以rejected狀態的promise來回傳給下一個Promise.then或者Promise.catch來接收，當他們接收到時，就會以非同步任務的形式來執行錯誤處理，確保另一個潛在的問題- 錯誤處理會不會致使callback的執行變成Zalgo`
<!--SR:!2023-09-12,12,190-->



















---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: