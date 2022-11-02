
## 描述



> expr1 && expr2
> Returns `expr1` if it can be converted to `false`; otherwise, returns `expr2`. Thus, when used with Boolean values, `&&` returns `true` if both operands are true; otherwise, returns `false`.



重點：
- expr1 && expr2 ：
	- 若expr1 和 expr2 本身是boolean value的話：
		- expr1 和 expr2 同為true，就expr1 && 
	- 若expr1 直接被判定成false或者經由轉換而可以判定成false，就會回傳(沒經由&&轉換的版本)expr1
	- 除此之外皆為回傳expr2


> expr1 || expr2
> Returns `expr1` if it can be converted to `true`; otherwise, returns `expr2`. Thus, when used with Boolean values, `||` returns `true` if either operand is true; if both are false, returns `false`.





## 複習


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: