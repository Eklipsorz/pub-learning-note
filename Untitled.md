## 實際使用Middleware Function

1. 實現能執行next()來調用下一個Middleware function的Middleware function會是以下形式，req和res分別為代表請求request和請求回應response這兩個物件，而next是指向函式物件的參數，系統會根據同個Middleware的function先後順序來自動決定，從最先辨識到的function來先執行，而funct1中的某一段放入next()的話，系統執行到那段便會由funct1呼叫另一個Middleware function，而該Middleware function由於共享著req和res，所以前者所做的變動，後者會看到，接著等到funct1的next()所呼叫的函式將控制權返回至funct1時，便會執行do something 2，

  

```

function funct1(req, res, next) {

// do something 1

  

next()

// do something 2

}

```

  

2. 實現結束cycle的方式主要方式為在同一個請求下的Middleware function進行回應請求，就即可結束cycle，但實際上還是依據 "回應給客戶端的內容是否依賴於最後一個middleware function要傳遞給客戶端的response物件" 來決定是否正式結束cycle，若依賴的話，內容得執行完最後一個middleware functionb讓物件和內容一併轉交過去；若不依賴的話，Middleware Function可以自行回應請求，根據這樣可以分為幾種形式：

  
  

- 回應客戶端內容依賴於response物件，而負責回應的middleware function是最後一個function：通常負責回應內容的middleware function會放在middleware中的最後一個function，而前面的middleware function會先處理回應內容所要做的事情(如驗證)，在這裡會先由funct1執行它的程式碼，接著由他呼叫funct2，然後再由funct2呼叫funct3，這情況會延續到functN，當執行functN時，functN透過render將回應內容放置response物件，等到執行完時，由它將response 物件(回應內容)一併轉交給客戶端。

```

// case1：

function funct1(req, res, next) {

// do something

next()

}

function funct2(req, res, next) {

// do something

next()

}

.

.

.

function functN(req, res) {

res.render(somthing)

}

```

  

- 回應客戶端內容依賴於response物件，但負責回應的middleware function不是最後一個的function

  
  
  

- 當前面的function已經做出回應但該function仍繼續執行著next()：當一個請求X被伺服器接收並轉換成request這個物件，由於同為同一個middleware的function會共享於request和response這兩個物件，所以只要任意一個function對request進行回應封包的發送，就能順利地結束請求X的cycle，但由於負責做出回應的function以及之後的function也做出了next()，而這情況會一直執行到第n個function才正式停止執行middleware function 的執行

```

// 前面的函式已經對請求X來回應，但該函式仍繼續執行next()

function functM(req, res, next) {

.

.

res.send(something) // 該函式會提前回應客戶端

.

.

next()

}

.

.

.

  

function functN(otherParameter) {

// do something1

}

```

  

- 做出回應的function

```

function functM(req, res) {

.

.

res.send(something)/res.rend(something)

.

.

}

```