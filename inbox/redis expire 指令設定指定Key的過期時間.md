## 描述
> -   `NX` -- Set expiry only when the key has no expiry
> -   `XX` -- Set expiry only when the key has an existing expiry
> -   `GT` -- Set expiry only when the new expiry is greater than current one
> -   `LT` -- Set expiry only when the new expiry is less than current one

重點：
- expiry 意指為過期時間
- 設定對對
 


```
EXPIRE key seconds 
```



## 複習

---
Status: 
Tags:
Links:
References:
[[@redisEXPIRE]]