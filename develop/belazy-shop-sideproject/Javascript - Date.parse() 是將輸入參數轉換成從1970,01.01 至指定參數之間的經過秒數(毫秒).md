
Javascript - Date.parse() 是將輸入參數轉換成從1970,01.01 至指定參數之間的經過秒數(毫秒)。語法形式如下：dateString 是以ISO1860 官方規定的日期字串形式(字串內容為日期)

```
Date.parse(dateString)
```

回傳值：
- 若dateString是合法的日期格式，就輸出經過毫秒
- 若dateString不是合法的日期格式，就輸出NaN
- 若dateString內是數字，仍有可能輸出經過毫秒
```
Date.parse('0')
// 946656000000
```


---
Status: #🌱 
Tags:
[[JavaScript]] - [[Side Project]]
Links:
References:
[[@DateParseJavaScript]]