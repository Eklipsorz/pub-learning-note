## 描述
> -   `NX` -- Set expiry only when the key has no expiry
> -   `XX` -- Set expiry only when the key has an existing expiry
> -   `GT` -- Set expiry only when the new expiry is greater than current one
> -   `LT` -- Set expiry only when the new expiry is less than current one

重點：
- expiry 意指為過期時間
- 設定對對
- NX
- XX
- GX
- LT


```
EXPIRE key seconds [ NX | XX | GT | LT]
```



## 複習
#🧠 Question :: ->->-> ``
<!--SR:!2022-06-11,3,250-->

---
Status: 
Tags:
Links:
References:
[[@redisEXPIRE]]