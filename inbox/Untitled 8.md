## 描述


### 表格的難點
- 表格本身具有較多狀態要管理，主要有validity和value
- validity得要考量什麼時候驗證以及ㄖ



### when to validate
主要有：
- 當表格提交時就驗證輸入欄位
- 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證
- 當使用者在輸入欄位輸入任意字元就驗證


#### 當表格提交時就驗證輸入欄位
> when form is submitted：
>- allows the user to enter a valid value before warning him/her 
>- avoid unnecessary warnings but maybe present feedback too late 

重點：
- 當表格提交時才開始驗證輸入欄位
- 警告訊息會等到使用者輸入完畢才顯示
- 優缺點：
	- 優點：可減少不必要的警告
	- 缺點：提醒使用者輸入是否正確的時機點太慢了
### 當使用者輸入完輸入欄位或者從特定輸入欄位失去焦點就驗證

> when a input is losing focus：
> - allows the user to enter a valid value before warning him/her 
> - very useful for untouched forms so where do you user hasn't entered anything yet.

重點：
- 當使用者輸入完輸入欄位才驗證輸入欄位，具體會是使用者從特定輸入欄位輸入完並轉移其他元件為active element才開始驗證
- 警告訊息會等到使用者輸入完畢才顯示
- 優缺點：
	- 優點：在使用鍵盤對元件的事件來說，不會將沒輸入過的欄位視為錯誤
	- 缺點：提醒使用者輸入是否正確的時機點稍慢了，因為還得等使用者從特定輸入欄位輸入完並轉移其他元件為active element才開始驗證





### 當使用者在輸入欄位輸入任意字元就驗證
> on every keystroke：
>- warns use before he/she had a chance of entering valid values 
>- if on the other hand we combine this  with other methods and we only validate on keystroke if the input was invalid before


重點：
- 當使用者在輸入欄位輸入任意字元就驗證
- 警告訊息會在使用者開始輸入時就呈現
- 優缺點：
	- 優點：即時告知使用者輸入的內容是否正確
	- 缺點：每一次輸入時就會開始驗證並提示，這容易造成不必要大量的錯誤提示，且一開始的輸入肯定會被判斷成錯誤的




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