## 描述


將callback交給非同步任務A來執行的問題：
- 太早執行callback：若任務A是以同步來執行callback，使callback擷取目前的資訊來執行
- 太晚執行callback：若任務A是以非同步來執行callback，這會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行。
- 呼叫callback的次數超過一次或者沒呼叫callback
- 沒有傳入任何必要的參數至callback
- 因callback執行時拋出錯誤而產生預期外的結果，比如吞掉callback執行時拋出的錯誤或者例外，非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理、因系統接受到錯誤而採取預設的錯誤處理，而錯誤處理是以同步執行來執行，而callback是以非同步來執行，顯然會使callback整體變成Zalgo


在Promise 中分別針對這幾個問題來增強執行callback的被信任程度

### 太早執行callback

> 太早執行callback：若任務A是以同步來執行callback，使callback擷取目前的資訊來執行


在Promise中，無論執行callback的方式是否為同步執行，都會因爲Promise.then的緣故全都以非同步來執行callback，換言之，會先等待Promise指定任務完成，接著執行callback
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

在Promise中，無論執行callback的方式是否為非同步而沒辦法在Promise指定任務完成後的指定時間內執行，都可以藉由promise.then給定的程式碼位置來由上至下按照位置順序去排程非同步任務callback，如下：Promise會製造fulfilled狀態或者rejected狀態的promise，並且呼叫其promise的then來讓callback1先執行，接著在執行callback2，最後在執行callback3
```
Promise(...)
.then(callback1, callback1)
.then(callback2, callback2)
.then(callback3, callback3)
```

### 呼叫callback的次數超過一次或者沒呼叫callback

> 呼叫callback的次數超過一次或者沒呼叫callback

callback適合的執行次數會是1次，而在Promise中，所有經由Promise.then所註冊的callback，只要該Promise被解析(resolve)或者被拒絕(rejected)，其對應的callback就只會因為Promise.then而被執行一次。

但不保證將相同callback註冊在多個Promise.then而產生出超過一次的callback之執行次數，然而執行次數的決定會是由註冊方來決定，而非交由原本無法信任的非同步任務A來決定

### 沒有傳入任何必要的參數至callback

> 沒有傳入任何必要的參數至callback

在Promise中，都會將fulfilled狀態或者rejected狀態的內容當作callback的參數來填入，所以只要設定fulfilled狀態或者rejected狀態的內容以及讓callback設定成合適形式的引數形式，就能確保callback能獲取到參數來執行。

### 吞掉callback執行時拋出的錯誤或者例外


> 吞掉callback執行時拋出的錯誤或者例外：非同步任務A執行callback時拋出錯誤，但沒有錯誤處理來處理

預期情況下，還有衍生出Zalgo問題機會，比如由系統的內建錯誤處理攔截到錯誤，並且以同步形式來執行錯誤，若callback本身就是非同步執行，那麼會使整體的callback(含錯誤處理)在執行上變成難以區分其執行方式的Zalgo

在Promise中，會將所有發生在callback上的錯誤和執行錯誤全以rejected狀態的promise來回傳給下一個Promise.then或者Promise.catch來接收，當他們接收到時，就會以非同步任務的形式來執行錯誤處理，確保另一個潛在的問題- 錯誤處理會不會致使callback的執行變成Zalgo


比如：當callback1執行時拋出錯誤時，這時系統會直接以fullfilled狀態的promise來呼叫它擁有的catch或者then來執行對應錯誤處理callback。
```
new Promise((resolve, reject) => {
	resolve(10);
})
.then(callback1)
.catch(callback2) // 或者 .then(callback1, callback1)
```



## 複習

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: