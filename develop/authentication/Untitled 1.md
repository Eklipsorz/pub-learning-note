## 描述


除了server-side session為主的登入驗證外，還有authentication tokens可以實現登入驗證


### authentication tokens 概念

1. 伺服器比對使用者所輸入的credential和資料庫上的credential是否一樣，若一樣就做下一步；若不一樣就不做

2. 建立permission token 給予客戶端 (token 的製作會使用hashing algorithm 和key 搭配credential來產生獨特且不可反解的hash 字串)

  

permission token的構成會是由使用者識別用的資料(如帳號)以及hash 字串，其hash字串會是由伺服器的hashing algorithm和伺服器儲存的key搭配識別用的資料來組合成獨特且不可反解的hash字串。

  

驗證時，客戶端會拿著token(含有識別用的資料和hash字串)來發送，伺服器收到就會拿識別用的字串和key、hashing algorithm來產生對應hash字串，並比對hash 字串和客戶端的token內存的內容是否一樣，若一樣就表示這token是由伺服器所產生，且未竄改；若不一樣就表示這token不是由伺服器產生，或者被篡改過的。

  

一樣的話，就會依照識別用的資料取得對應使用者的完整資料。

  

接著客戶端可以在request 封包內夾雜著permission token來向後端伺服器索要受保護的資源


## 複習


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
[[登入驗證可使用server-side session來實現，並將請求封包處理內容儲存在session並賦予id至客戶端來當作access，好方便客戶端利用access存取]]
References:
