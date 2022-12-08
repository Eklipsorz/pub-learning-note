## 描述


> 可以使用CNAME記錄將「bar.example.com」指向「foo.example.com」。因此，可能會有人隨意的將bar.example.com稱作是foo.example.com的「CNAME」。然而事實並非如此，bar.example.com的「CNAME」是foo.example.com，因為CNAME的意思是真實名稱，而右側才是真實名稱，才是CNAME。


> 這則誤會在《[RFC 2181](https://tools.ietf.org/html/rfc2181)》「DNS規範的解釋」一章中有提到。應當說左側標籤是右側真實名稱的一個同名。即下述CNAME記錄：

> bar.example.com.        CNAME  foo.example.com.

  
> 應當讀作：

> bar.example.com的真實名稱是foo.example.com。請求訪問bar.example.com的客戶端會得到foo.example.com返回的結果。


[[@cambridgedictionaryTransactionTranslationTraditional]]
> A Canonical Name record (abbreviated as CNAME record) is a type of resource record in the Domain Name System (DNS) that maps one domain name (an alias) to another (the canonical name).[1]

Canonical命名緣由
> accepted as being true, correct and established

重點：
- Canonical 含義為以清楚正確的形式被人接受的，換言之為(被xxx接收為)真實的
- Canonical Name 在域名系統是ˋ


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱  
Tags:
[[DNS]]
Links:

References:
[[@cambridgedictionaryTransactionTranslationTraditional]]