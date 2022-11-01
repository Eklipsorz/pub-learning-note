## 描述
[[@WuJianDeShiYongJavaScriptMDN]]

```
var obj = { property_1:   value_1,   // property_# may be an identifier...
            2:            value_2,   // or a number...
            // ...,
            'property n': value_n }; // or a string
```

> where `obj` is the name of the new object, each `property_i` is an identifier (either a name, a number, or a string literal), and each `value_i` is an expression whose value is assigned to the `property_i`.



> An object property name can be any valid JavaScript string, or anything that can be converted to a string, including the empty string. However, any property name that is not a valid JavaScript identifier(for example, a property name that has a space or a hyphen, or that starts with a number)

重點：
- JS 物件上的屬性名稱可以是字串、單純名稱、單純數字，至於開放原因為：屬性名稱本質上是字串，只是額外開放其他可以直接被轉換成字串的資料型別來表示屬性名稱
	- 字串：會是以兩個單引號或者兩個雙引號包住的內容，含空字串
	- 單純名稱：未添加單引號或者雙引號來包住、也並非是數字的內容
	- 單純數字：內容只有數字
- 但不是每個單純名稱都能當合法屬性名稱，因為容易造成系統上的誤解，比如空白、連字號、以數字為開頭的名稱、字串
- 每一次對於物件的屬性進行存取，都會先將屬性名稱通通轉換成字串來存取正確對應屬性名稱
- 形式：
	- 字串
	```
	const object = {
		'property1': value1
	}
	
	console.log(object['property1'])
	```
	- 單純名稱
	```
	const object = {
		property: value1
	}
	
	console.log(object['property1'])
	```
	- 單純數字
	```
	const object = {
		1: value1
	}
	
	console.log(object['1'])
	```
## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@WuJianDeShiYongJavaScriptMDN]]