## 描述


問題為驗證字串原本是否為日期字串(Date string)，在這裡只考慮著內為含有年、月、日、星期幾、小時、分鐘、秒數，且輸入肯定是按照這格式來處理，其餘有可以判定為日期字串皆不在內，比如字串內容為1，可以被判定為日期字串

### 日期字串(Date String)
1. 字串內容為日期格式內容的字串，就稱之為日期字串
2. 格式上會含有年月日小時分鐘秒數，部分單純數字也會被誤判成日期字串
3. 通常日期字串的格式規定是依據制定標準的組織來統一制定


### 考慮點
1. 由於規格上和輸入上都確定為日期內容會有年、月、日、星期幾、小時、分鐘、秒數格式的內容，所以只需要考慮其他系統上會用到的資料型別是否會被誤判
2. 系統上會誤判為日期字串的資料型別只有數字字串。

### 解法
解法思路為：
- 檢查比對值是否為單純數字字串，若是的話，就回傳false；若不是，就繼續下一個檢查
- 透過Date.parse來解析可能是日期字串的字串是否真為日期字串，若是的話，就回傳true；反之，回傳false

```
static isDateString(value) {
	const { isNumberString } = ParameterValidationKit
	if (isNumberString(value)) return false
	return Boolean(Date.parse(value))
}
```


## 複習
#🧠 JavaScript 日期字串是什麼？ ->->-> `字串內容為日期格式內容的字串，就稱之為日期字串`
<!--SR:!2024-02-09,227,230-->
#🧠 JavaScript 日期字串格式上是誰制定的？ ->->-> `日期字串的格式規定是依據制定標準的組織來統一制定`
<!--SR:!2023-11-22,320,250-->

#🧠 JavaScript 日期字串格式上通常會有什麼？ ->->-> `年、月、日、小時、分鐘、秒數`
<!--SR:!2024-03-26,396,250-->

#🧠  單純數字有沒有可能會被視為日期字串格式，舉一個例子->->-> `有可能，比如說數字1`
<!--SR:!2023-12-02,325,250-->

#🧠 JavaScript 如何在輪流對數字字串、日期字串、字串進行檢查下驗證字串內容原本是否為日期字串的方法思路為何（假如規格和輸入都確定是日期內容會有年、月、日、星期幾、小時、分鐘、秒數格式)->->-> `檢查比對值是否為單純數字字串，若是的話，就回傳false；若不是，就繼續下一個檢查、透過Date.parse來解析可能是日期字串的字串是否真為日期字串，若是的話，就回傳true；反之，回傳false`
<!--SR:!2023-07-11,93,230-->

#🧠 JavaScript 驗證字串內容原本是否為日期字串的方法之對應實現程式碼是什麼(數字字串會不會被當成日期？ 該方法可能用來檢測一般字串，且若有日期字串的話，那麼日期字串會是以年月日星期幾時分秒格式) ->->-> `if (isNumberString(value)) return false、	return Boolean(Date.parse(value))`
<!--SR:!2023-07-17,182,250-->


#🧠 JavaScript 驗證字串內容原本是否為日期字串的方法之對應實現程式碼是什麼( 該方法可能用來檢測一般字串，且若有日期字串的話，那麼日期字串會是以年月日星期幾時分秒格式) ->->-> `if (isNumberString(value)) return false、	return Boolean(Date.parse(value))`
<!--SR:!2023-05-12,139,250-->


---
Status: #🌱 
Tags:
[[JavaScript]] - [[Side Project]]
Links:
[[驗證字串內容原本是否為數字字串的方法就是先將比對值以Number轉換，接著再以其結果轉換String比對原本轉換前的內容是否一致，一致則為Number String]]
References: