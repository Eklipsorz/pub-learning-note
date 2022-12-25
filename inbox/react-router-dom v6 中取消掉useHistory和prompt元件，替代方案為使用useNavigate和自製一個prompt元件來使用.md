## 描述



### 版本：實現 programmatically navigate 功能：

1. 在v5 使用 useHistory
2. 在v6 使用 useNavigate，其中useHistory被移除

###  v6：useNavigate 語法

useNavigate：
- 用途：在v6給予開發者一個藉由執行程式碼讓使用者導向至特定頁面
- 用法為
	- useNavigate 會回傳一個函式物件
	- 該函式物件會有兩個引數
		- path 為指定要導向的頁面網址 或者填入數字，若為數字就代表會以目前頁面A網址在stack上位置來位移，若為-1就往頁面A的上一頁來導向；若為-2就往頁面A之上一頁的上一頁來導向；若為1就往頁面A的下一頁來導向
		- options 為設定物件，專門設定如何導向，其中常見屬性為replace，若為true的話，就以replace來導向，否則就預設用push來導向
```
1.  const navigate = useNavigate()
2.  navigate(path, options)
```

### prompt 元件在v6的情況
prompt 在 v6 被移除



## 複習

#🧠 在react-router-dom中的版本中：版本5和版本6實現 programmatically navigate 功能有哪些？ ->->-> `v5是使用useHistory、v6是使用useNavigate`
<!--SR:!2022-12-31,6,230-->

#🧠 react-router-dom v6 中還有沒有useHistory和prompt元件，若沒有的話有何種替代->->-> `版本5沒有useHistory和prompt元件，替代方案為使用useNavigate和自製一個prompt元件來使用`
<!--SR:!2023-01-21,27,250-->

#🧠 react-router-dom v6 ：useNavigate 是什麼？ ->->-> `在v6給予開發者一個藉由執行程式碼讓使用者導向至特定頁面`
<!--SR:!2022-12-25,10,250-->

#🧠 react-router-dom v6 ：useNavigate 用法 是什麼？ ->->-> `const navigate = useNavigate()`
<!--SR:!2023-01-22,28,250-->

#🧠 react-router-dom v6 ：useNavigate 會回傳什麼？ ->->-> `會回傳可以將使用者導向至指定頁面的函式物件`
<!--SR:!2023-01-17,24,250-->


#🧠 react-router-dom v6 ：useNavigate 會回傳什麼樣的函式物件 ->->-> `會回傳可以將使用者導向至指定頁面的函式物件`
<!--SR:!2023-01-22,28,250-->

#🧠 react-router-dom v6 ：useNavigate 回傳的函式物件夾帶的引數是什麼？ ->->-> `path 為指定要導向的頁面網址 或者填入數字、options 為設定物件，專門設定如何導向`
<!--SR:!2023-01-15,23,250-->

#🧠 react-router-dom v6 ：useNavigate 回傳的函式物件夾帶的引數path若是數字，會如何表示？ 1會是如何？ -1又會是如何？ ->->-> `若為數字就代表會以目前頁面A網址在stack上的位置來位移，若為-1就往頁面A的上一頁來導向；若為-2就往頁面A之上一頁的上一頁來導向；若為1就往頁面A的下一頁來導向`
<!--SR:!2022-12-25,10,250-->



---
Status: #🌱 
Tags:
[[React]]
Links:
References: