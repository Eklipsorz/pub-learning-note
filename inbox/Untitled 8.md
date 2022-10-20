## 描述



表格需要關注的點：
- 驗證輸入並給予回饋


### when to validate
主要有：
- 當表格提交時就驗證輸入欄位
- 當

### 
when form is submitted：

- allows the user to enter a valid value before warning him/her (允許使用者在沒收到任何警告的情況下按下提交)

- avoid unnecessary warnings but maybe present feedback too late (好處是減少不必要的警告，壞處為提醒使用者輸入是否正確的時機點太慢)


###

when a input is losing focus：

- very useful for untouched forms (好處是非常適用於從沒動過(輸入過)的表格，因為不會直接提示這些沒動過的輸入欄位為錯誤的； 壞處是驗證使用者輸入內容必須要等到使用者輸入完成並且切換成另一個元件為active element才會去驗證)


###
on every keystroke：

- warns use before he/she had a chance of entering valid values (每一次輸入時就會開始驗證並提示，這容易造成不必要大量的錯誤提示，且一開始的輸入肯定會被判斷成錯誤的)

- if on the other hand we combine this  with other methods and we only validate on keystroke if the input was invalid before

  

if applied only on invalid inputs, has the potential of providing more direct feedback

###
because to question then is when to validate, when should you check the user input?

(什麼時候驗證使用者所輸入的？）

- 當表單提交時 (when form is submitted)

- 當使用者一旦從指定輸入欄至轉移其他元件為active element (you can also check the value entered by a user when a input is losing focus)

- 當使用者每一次輸入時(on every keystroke)


###  通常輸入欄位值不合法的話

> one or more inputs are invalid：
> - output input-specific error messages & highlight problematic inputs
> - ensure form can't be submitted/saved


重點：
- 呈現錯誤時會有的樣式和畫面，比如會有錯誤訊息和用顏色標註錯誤的輸入欄
- 存在錯誤輸入欄位值的表格內容是不被允許提交


### 通常輸入欄位合法的話
 
> all inputs are valid：
> - all form to be submitted/saved

重點：
- 若都合法的話，表格內容是被允許提交

###  form 和input 這兩者本身擁有多種狀態

- 輸入欄的狀態主要分為validity 和 value 這兩種，有N個輸入欄就有2N個狀態
- 表格整體的狀態分為validity ，會依據所有輸入欄位是否都正確來判定：
	- 任一輸入欄不合法就即為表格不合法
	- 所有的輸入欄都合法就即為表格合法

- form is invalid or valid：根據所有輸入欄位是否都正確來判定，有任一不合法就即為表格不合法，全合法就表格合法

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: