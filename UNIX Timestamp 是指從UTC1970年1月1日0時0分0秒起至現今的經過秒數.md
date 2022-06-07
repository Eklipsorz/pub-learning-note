

## 描述
[[@wikidataUnixTime2022]]
> **Unix time** (also known as **Epoch time**, **Posix time**,[1] **seconds since the Epoch**,[2] or **UNIX Epoch time**[3]) is a system for describing a point in time. It is the number of seconds that have elapsed since the _Unix epoch_, excluding leap seconds. The Unix epoch is 00:00:00 UTC on 1 January 1970 (an arbitrary date).



UNIX Timestamp 是指從UTC1970年1月1日0時0分0秒起至現今的經過秒數

Timestamp 的 Time 是指時間，stamp為印記，合併起來以時間為內容的印記或者標記時間的印記

> **a record in printed or digital form that shows the time at which something happened or was done**

Javascript 的Date 換算方式為以下，使用Date物件所獨有的getTime方法來得到從
UTC1970年1月1日0時0分0秒起至指定時間的毫秒數，而若要獲取一般秒數，如單純的1秒、2秒、3秒的話，就得除以1000來換算，接著在用floor來得到實際經過的秒數
```
Math.floor((new Date(...)).getTime()/1000)
```

使用floor是為了確實得到實際經過的秒數，而不是做進位來得到不一致的值。
```javascript
var date = new Date('2012.08.10');
var unixTimeStamp = Math.floor(date.getTime() / 1000);
```

> In this case it's important to return only a whole number (so a simple division won't do), and also to only return actually elapsed seconds (that's why this code uses `Math.floor()` and not `Math.round()`).

## 複習
#🧠 Question :: ->->-> ``

---
Status: #📥 
Tags:
Links:
References:
[[@wikidataUnixTime2022]]