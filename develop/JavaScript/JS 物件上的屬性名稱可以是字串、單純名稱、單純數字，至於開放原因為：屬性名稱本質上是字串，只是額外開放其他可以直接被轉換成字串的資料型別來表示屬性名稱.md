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
- JS 物件上的屬性名稱可以是字串、名稱、數字，至於開放原因為：屬性名稱本質上是字串，只是額外開放其他可以直接被轉換成字串的資料型別來表示屬性名稱
	- 字串：會是以兩個單引號或者兩個雙引號包住的內容，含空字串
	- 名稱(name)：未添加單引號或者雙引號來包住、也並非是數字的內容
	- 數字：內容只有數字
- 但不是每個名稱都能當合法屬性名稱，因為容易造成系統上的誤解，比如空白、連字號、以數字為開頭的名稱
- 每一次對於物件的屬性進行存取，都會先將屬性名稱通通轉換成字串來存取正確對應屬性名稱
- 形式：
	- 字串
	```
	const object = {
		'property1': value1
	}
	
	console.log(object['property1'])
	```
	- 名稱
	```
	const object = {
		property: value1
	}
	
	console.log(object['property1'])
	```
	- 數字
	```
	const object = {
		1: value1
	}
	
	console.log(object['1'])
	```
## 複習

#🧠 JS物件的屬性名稱可以填入什麼型別？->->-> `字串、名稱、數字`
<!--SR:!2023-09-07,194,250-->

#🧠 JS物件的屬性名稱的型別最主要是什麼型別？ ->->-> `屬性名稱本質上是字串`
<!--SR:!2024-12-30,483,250-->

#🧠 JS物件的屬性名稱可以填入字串、數字、名稱這些型別，為什麼？->->-> `屬性名稱本質上是字串，只是額外開放其他可以直接被轉換成字串的資料型別來表示屬性名稱`
<!--SR:!2024-09-21,418,250-->

#🧠 JS物件的屬性名稱可以填入字串、數字、名稱這些型別，其中名稱是什麼？>->-> `未添加單引號或者雙引號來包住、也並非是數字的內容`

#🧠 JS 物件屬性名稱型別：字串 vs 名稱之間差別->->-> `一個是使用雙引號或者單引號來標注；另一個是沒用`
<!--SR:!2023-09-07,194,250-->


#🧠  JS物件的屬性名稱可以填入字串、數字、名稱這些型別，其中名稱可以填入任何內容嗎？->->-> `並不能，容易造成系統上誤解的內容都不行，比如空白、連字號、以數字為開頭的名稱`
<!--SR:!2024-02-27,224,230-->


#🧠 JS：針對物件的特定屬性存取時，JS會做什麼型別轉換？ ->->-> `每一次對於物件的屬性進行存取，都會先將屬性名稱通通轉換成字串來存取正確對應屬性名稱`
<!--SR:!2024-08-04,383,250-->

#🧠 JS：物件的屬性名稱型別若是字串會是什麼形式以及如何存取？舉例來說 ->->-> `const object = { 'property1': value1 } console.log(object['property1'])`
<!--SR:!2024-10-23,440,250-->

#🧠 JS：物件的屬性名稱型別若是名稱會是什麼形式以及如何存取？舉例來說->->-> `const object = { property1: value1 } console.log(object['property1'])`
<!--SR:!2024-11-25,459,250-->

#🧠 JS：物件的屬性名稱型別若是數字會是什麼形式以及如何存取？舉例來說->->-> `const object = { 1: value1 } console.log(object['1'])`
<!--SR:!2024-09-19,416,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@WuJianDeShiYongJavaScriptMDN]]