
## 描述


### expr1 && expr2 
> expr1 && expr2
> Returns `expr1` if it can be converted to `false`; otherwise, returns `expr2`. Thus, when used with Boolean values, `&&` returns `true` if both operands are true; otherwise, returns `false`.



重點：
- expr1 && expr2 ：
	- 若expr1 和 expr2 本身是boolean value的話：
		- expr1 和 expr2 同為true，就expr1 && expr2 結果為true
		- 其餘狀況皆回傳false
	- 若expr1 和 expr2 這兩者有任一個不為boolean value的話
		- expr1 可經由轉換而判定成false，就會回傳(沒經由&&轉換的版本)expr1
		- 除此之外皆為回傳expr2

### expr1 || expr2

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


## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: