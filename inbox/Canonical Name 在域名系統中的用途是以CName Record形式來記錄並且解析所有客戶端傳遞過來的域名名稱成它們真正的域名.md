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
- DNS Record 是DNS 系統用來解析接收過來域名會是什麼的紀錄內容
- Canonical 含義為以清楚正確的形式被人接受的，換言之為(被xxx接收為)真實的
- Canonical Name 在域名系統中的用途是：
	- 以DNS Record 來替特定域名取別名，而別名的形式會是網域形式
		- 別名會以CName Record來記錄
	- 當客戶端以別名來給DNS解析時，DNS會檢查自己的CName Record是否有這個，若有就以對應名稱來轉遞；若沒有就告知沒有
- 替特定域名取別名的方式為
	- 形式會是如下：host為別名、CName為關鍵字、value會是指別名的真實名字
```
host CName Value 
```
- 範例：若設定如下，會將bar.example.com 的真實名稱解析成foo.example.com，也就是看到bar.example.com，直接被系統看作是foo.example.com.
```
bar.example.com.        CNAME  foo.example.com.
```

## 複習
#🧠 Canonical命名緣由是什麼？ ->->-> `以清楚正確的形式被人接受的，換言之為(被xxx接收為)真實的`
<!--SR:!2023-04-24,50,210-->

#🧠 Canonical Name 在域名系統中的用途是(紀錄、比對) ->->-> `以DNS Record 來替特定域名取別名、 當別人以別名來給DNS解析時，DNS會檢查自己的CName Record是否有這個，若有就以對應名稱來轉遞；若沒有就告知沒有`
<!--SR:!2023-08-10,149,250-->

#🧠 Canonical Name 在域名系統中的用途是 ->->-> `以DNS Record 來替特定域名取別名、 當別人以別名來給DNS解析時，DNS會檢查自己的CName Record是否有這個，若有就以對應名稱來轉遞；若沒有就告知沒有`
<!--SR:!2023-04-22,72,230-->

#🧠 Canonical Name 在域名系統中的用途是以DNS Record 來替特定域名取別名，具體會是什麼？ ->->-> `會將別名和實際名稱綁定在一塊，並記錄成CName Record`
<!--SR:!2023-04-04,73,250-->

#🧠 Canonical Name 在域名系統中的用途是當別人以別名來給DNS解析時，具體會是做什麼？->->-> `DNS會檢查自己的CName Record是否有這個，若有就以對應名稱來轉遞；若沒有就告知沒有`
<!--SR:!2023-04-04,66,230-->

#🧠 Canonical Name 在域名系統中的用途是以DNS Record 來替特定域名取別名和解析比對，其取別名的形式會是什麼？ ->->-> `host CName Value `
<!--SR:!2023-04-03,72,250-->

#🧠 Canonical Name 在域名系統中的用途是以DNS Record 來替特定域名取別名和解析比對，其取別名的形式會是host CName Value，請解釋這三個在做什麼？->->-> `host為域名形式的別名、CName為關鍵字、value會是指別名的真實域名形式名稱`
<!--SR:!2023-08-31,164,250-->

#🧠 若設定如下：bar.example.com.   CNAME  foo.example.com.，那麼系統會是如何解析？->->-> `會將bar.example.com 的真實名稱解析成foo.example.com，也就是看到bar.example.com，直接被系統看作是foo.example.com.`
<!--SR:!2023-07-13,132,250-->

#🧠 DNS Record 會是什麼？ ->->-> `DNS Record 是DNS 系統用來解析接收過來域名會是什麼的紀錄內容`
<!--SR:!2023-03-23,65,250-->

#🧠 CName Record 會是什麼？ ->->-> `屬於DNS Record的一種， 是紀錄著特定域名和別名的對應關係`
<!--SR:!2023-04-05,74,250-->


---
Status: #🌱  
Tags:
[[DNS]]
Links:

References:
[[@cambridgedictionaryTransactionTranslationTraditional]]