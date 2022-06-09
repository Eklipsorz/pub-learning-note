

Belazy - 確保讀取的值是否為0或者空值，這兩者在布林值都會呈現false
```
{
	"price": 0,
	"quantity": 0,
	"restQuantity": 0
}
```

經過下面這段
```
if (!quantity || !restQuantity || !price) {
	messageQueue.push('所有欄位都要填寫')
}
```

會呈現
```
messageQueue.push('所有欄位都要填寫')
```

而若真的沒填寫的話
```
{
	"price": "",
	"quantity": "",
	"restQuantity": ""
}
```
會呈現
```
messageQueue.push('所有欄位都要填寫')
```

## 解法
試著解析對方是否為人眼可辨別的數字，若是數字就給予跳過，否則就得到錯誤訊息

---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: