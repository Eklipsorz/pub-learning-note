
## 描述
由於考慮到欄位為空才會觸發，結果欄位值為0也會觸發，這對於判斷欄位是未填寫的目標是起衝突的

```
if (!quantity) {
	messageQueue.push('所有欄位都要填寫')
}
```

解法為：
	- 先轉換成字串，並判斷是否為''
```
static isFilledField(field) {
	const string = field.toString()
	return string !== ''
}
```


```
if (!isFilledField(quantity))
	messageQueue.push('所有欄位都要填寫')
}
```



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Side Project]]
Links:
References: