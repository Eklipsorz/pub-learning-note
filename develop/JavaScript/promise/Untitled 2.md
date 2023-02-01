## 描述


將callback交給非同步任務A來執行的問題：
- 太早執行callback：callback本身會是同步任務，任務A執行它就任由同步來執行，使callback擷取目前的資訊來執行
- 太晚執行callback：callback本身會是非同步任務，任務A執行它就任由非同步來執行，這會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行。
- 呼叫callback的次數超過一次或者沒呼叫callback
- 沒有傳入任何必要的參數
- 吞掉callback執行時拋出的錯誤或者例外


在Promise 中分別針對這幾個問題來增強執行callback的被信任程度

### 太早執行callback

> 太早執行callback：callback本身會是同步任務，任務A執行它就任由同步來執行，使callback擷取目前的資訊來執行


在Promise中，無論callback本身是否為同步，都會因爲Promise.then的緣故全都以非同步來執行callback，換言之，會先等待Promise指定任務完成，接著執行callback
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

> 太晚執行callback：callback本身會是非同步任務，任務A執行它就任由非同步來執行，這會因爲排程緣故而使callback的執行被排到很後頭，甚至被其他任務給插隊執行，無法及時以適當的時機點執行。

在Promise中，無論callback本身是否為非同步而沒辦法在Promise指定任務完成後的指定時間內執行，都可以藉由promise.then給定的程式碼位置來由上至下按照位置順序去排程非同步任務callback，如下：Promise會製造resolvecallback1先執行，接著在執行callback2，最後在執行callback3
```
Promise(...)
.then(calback1)
.then(callback2)
.then(callback3)
```

## 複習

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: