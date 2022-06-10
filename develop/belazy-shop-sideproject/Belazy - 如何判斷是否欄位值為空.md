
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
#🧠 若考慮要圖中的程式碼來驗證quantity欄位是否空值？請問還有重構空間嗎(提示：數字0)![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654774739/blog/javascript/String/empty-field-problem_g52iqy.png) ->->-> `有，考慮到數字0也能觸發，所以必須先轉換字串重新比較原字串才能達成`
<!--SR:!2022-06-13,3,250-->

#🧠 這兩個程式碼都是實現在欄位空值驗證，請問差異在哪![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654774739/blog/javascript/String/empty-field-problem-solution_tcesu5.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654774739/blog/javascript/String/empty-field-problem_g52iqy.png)->->-> `後者是欄位值為0也會觸發，這對於判斷欄位是未填寫的目標是起衝突的，前者是不會`

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Side Project]]
Links:
References: