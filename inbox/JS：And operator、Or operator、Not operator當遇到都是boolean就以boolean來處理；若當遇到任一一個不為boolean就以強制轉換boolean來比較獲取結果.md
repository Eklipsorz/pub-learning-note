
## 描述


### expr1 && expr2 
[[@mdnLogicalJavaScriptMDN]]
> expr1 && expr2
> Returns `expr1` if it can be converted to `false`; otherwise, returns `expr2`. Thus, when used with Boolean values, `&&` returns `true` if both operands are true; otherwise, returns `false`.



重點：
- expr1 && expr2 ：
	- 若expr1 和 expr2 本身是boolean value的話：
		- expr1 和 expr2 同為true，就expr1 && expr2 結果為true
		- 其餘狀況皆回傳false
	- 若expr1 和 expr2 這兩者有任一個不為boolean value的話
		- expr1 可經由Boolean強制轉換而判定成false，就會回傳(沒經由&&轉換的版本)expr1
		- 除此之外皆為回傳expr2

### expr1 || expr2
[[@mdnLogicalJavaScriptMDNa]]
> expr1 || expr2
> Returns `expr1` if it can be converted to `true`; otherwise, returns `expr2`. Thus, when used with Boolean values, `||` returns `true` if either operand is true; if both are false, returns `false`.

重點：
- expr1 || expr2：
	- 若expr1 和 expr2 本身是boolean value的話：
		- expr1  或者 expr2 有任一者為true的話，就expr1 || expr2 結果為true
		- 其餘狀況皆回傳false
	- 若expr1 和 expr2 這兩者有任一個不為boolean value的話
		- expr1 可經由轉換而判定成true，就會回傳(沒經由&&轉換的版本)expr1
		- 否則皆回傳expr2


### !expr1

[[@mdnLogicalNOTJavaScript]]
> The logical NOT (`!`) operator (logical complement, negation) takes truth to falsity and vice versa. It is typically used with boolean (logical) values. When used with non-Boolean values, it returns `false`if its single operand can be converted to `true`; otherwise, returns `true`.


重點：
- !expr1：
	- 若expr1本身為boolean value的話
		- expr1若為false，!expr1為true
		- expr1若為true，!expr1為false
	- 若expr1本身不為boolean value的話
		- expr1 會先以boolean value的形式來強制轉換，若為true，就回傳false
		- 若結果為false，就回傳true

## 複習
#🧠 JS： expr1 && expr2 會如何處理和回傳？若expr1 和 expr2 本身是boolean value->->-> `		- expr1 和 expr2 同為true，就expr1 && expr2 結果為true - 其餘狀況皆回傳false`

#🧠 JS： expr1 && expr2 會如何處理和回傳？若expr1 和 expr2 這兩者有任一個不為boolean value的話 ->->-> `		- expr1 可經由Boolean強制轉換而判定成false，就會回傳(沒經由&&轉換的版本)expr1 - 除此之外皆為回傳expr2`

#🧠 JS： 2 && console.log('hi') 會如何處理和回傳？為什麼？ ->->-> `會得到undefined，原因在於2會被判定成true，所以回傳值肯定會是以console.log('hi')為主，其回傳會是undefined`


#🧠 JS： 0 && console.log('hi') 會如何處理和回傳？為什麼？->->-> `會得到0，原因在於2會被判定成false，所以回傳值肯定會是0`

#🧠 JS： res && console.log('hi');  !res && console.log('hi !') 會如何處理和回傳？假若res為0的話->->-> `第一個回傳0，第二個會回傳undefined`


#🧠 JS： res && console.log('hi');  !res && console.log('hi !') 會如何處理和回傳？假若res為1的話 ->->-> `第一個會回傳undefined，第二個會回傳false`



#🧠  JS： expr1 || expr2 會如何處理和回傳？若expr1 和 expr2 本身是boolean value ->->-> `expr1  或者 expr2 有任一者為true的話，就expr1 || expr2 結果為true；其餘狀況皆回傳false`

#🧠 JS： expr1 || expr2 會如何處理和回傳？若expr1 和 expr2 這兩者有任一個不為boolean value的話->->-> `- expr1 可經由轉換而判定成true，就會回傳(沒經由&&轉換的版本)expr1 - 否則皆回傳expr2`

#🧠 JS： 2 || console.log('hi') 會如何處理和回傳？為什麼？ ->->-> `會回傳2，由於第一個會被判定成true，因而回傳2`

#🧠 JS： 0 || console.log('hi') 會如何處理和回傳？為什麼？ ->->-> `會回傳undefined，由於第一個會被判定成false，因而回傳console.log帶有的undefined`

#🧠 JS： res || console.log('hi');  !res || console.log('hi !') 會如何處理和回傳？假若res為0的話 ->->-> `第一個會是undefined，第二個會是true`

#🧠 JS： res || console.log('hi');  !res || console.log('hi !') 會如何處理和回傳？假若res為1的話 ->->-> `第一個會是1，第二個會是undefined`


#🧠 JS：!expr1 的 !稱之為什麼operator？ ->->-> `logical not operator !`

#🧠 JS： !expr1  的expr1 是非boolean，如何處理->->-> `強制轉換`

#🧠 JS： expr1 && expr2  的expr1和expr2 中有一個不為boolean，如何處理->->-> `強制轉換`

#🧠 JS： expr1 || expr2  的expr1和expr2 中有一個不為boolean，如何處理->->-> `強制轉換`


#🧠 JS：logical not operator會用什麼當作運算符號 ->->-> `!`

#🧠 JS： expr1 && expr2的&& 稱之為什麼operator ->->-> `logical and operator`

#🧠 JS： expr1 || expr2的|| 稱之為什麼operator ->->-> `logical or operator`

#🧠 JS：logical "OR" operator 會用什麼當作運算符號？ ->->-> `||`


#🧠 JS：logical "And" operator 會用什麼當作運算符號？ ->->-> `&&`

#🧠 JS： !expr1 會如何處理和回傳？若expr1 本身是boolean value ->->-> `	- 若expr1本身為boolean value的話 - expr1若為false，!expr1為true - expr1若為true，!expr1為false`


#🧠 JS： !expr1 會如何處理和回傳？若expr1 本身不是boolean value->->-> `	- 若expr1本身不為boolean value的話 - expr1 會先以boolean value的形式來強制轉換，若為true，就回傳false - 若結果為false，就回傳true`

#🧠 JS： !expr1 都一律回傳什麼？或者按照情況回傳不同的東西 ->->-> `都一率回傳true或者false`

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:

References:
[[@mdnLogicalNOTJavaScript]]
[[@mdnLogicalJavaScriptMDNa]]
[[@mdnLogicalJavaScriptMDN]]