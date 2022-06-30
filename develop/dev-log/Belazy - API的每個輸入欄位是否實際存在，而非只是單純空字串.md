## 描述
若客戶端沒指定特定欄位或者屬性值給予伺服器，比如輸入要求輸入password、checkPassword這兩個欄位值，然而實際給予伺服器的資料會是：
	- 沒有password、checkPassword欄位值

```
{

}
// or
{
	otherProperties:....	
}
```


若給予express server來解析的話，會得到undefined
```
const { password, checkPassword } = req.body
```


### 可能修改方向

1.  為此可以根據undefined來判定實際資料是否真有指定欄位

```
function isUndefined(value) {
	return value === undefined
}
```
2. 延續第一方法，再結合isFilledField(value)來重構成新的檢驗方式來修改


### bug潛藏位置
目前bug是存在各個需要參數的API

### bug重要性
medium


---
Status: #🌱 
Tags:
[[Bug]] - [[Dev-log]]
Links:
References: