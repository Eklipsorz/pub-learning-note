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


在Promise中，無論callback是否為同步，都執行ㄒㄧㄝ

## 複習

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: