## 描述



表格需要關注的點：
- 驗證輸入並給予回饋

### 
when form is submitted：

- allows the user to enter a valid value before warning him/her (允許使用者在沒收到任何警告的情況下按下提交)

- avoid unnecessary warnings but maybe present feedback too late (好處是減少不必要的警告，壞處為提醒使用者輸入是否正確的時機點太慢)


###

when a input is losing focus：

- very useful for untouched forms (好處是非常適用於從沒動過(輸入過)的表格，壞處是驗證使用者輸入內容必須要等到使用者輸入完成並且切換成另一個元件為active element才會去驗證)


###
because to question then is when to validate, when should you check the user input?

(什麼時候驗證使用者所輸入的？）

- 當表單提交時 (when form is submitted)

- 當使用者一旦從指定輸入欄至轉移其他元件為active element (you can also check the value entered by a user when a input is losing focus)

- 當使用者每一次輸入時(on every keystroke)


### 

one or more inputs are invalid：

- output input-specific error messages & highlight problematic inputs

- ensure form can't be submitted/saved

  

all inputs are valid：

-

- all form to be submitted/saved


###



1. form 和input 這兩者本身擁有多種狀態

> one or more inputs are invalid

- input is invalid or valid ： 輸入欄位目前值是否正確，

- form is invalid or valid：根據所有輸入欄位是否都正確來判定，有任一不合法就即為表格不合法，全合法就表格合法

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: