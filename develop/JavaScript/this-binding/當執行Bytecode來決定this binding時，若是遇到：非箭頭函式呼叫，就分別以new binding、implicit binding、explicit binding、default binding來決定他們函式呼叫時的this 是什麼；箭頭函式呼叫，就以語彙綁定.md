## 描述


當執行Bytecode來決定this binding時，若是遇到
	- 非箭頭函式呼叫，就分別以new binding、implicit binding、explicit binding、default binding來決定他們函式呼叫時的this 是什麼
	- 箭頭函式呼叫，就以語彙綁定來決定this是什麼

this binding 對於函式是決定了 **每個函式在呼叫時所用的this會是什麼**


### 非箭頭函式呼叫

[[若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定：explicit binding > implicit binding > default binding 和 new binding > implicit binding > default binding]]
[[new binding 是由new operator 主導來建立一個物件並以此物件作為特定函式呼叫的this]]
[[JS：explicit binding 是相較於implicit binding而言，較為直接且明確告知this是設定什麼]]
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
[[JS：default this binding 是指當沒有使用任何一個方法來進行this binding就採用的預設方式]]


### 箭頭函式呼叫

[[箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫]]

## 複習
#🧠 this binding 對於函式來說是什麼？ ->->-> `決定了 **每個函式在呼叫時所用的this會是什麼**`
<!--SR:!2023-02-01,72,250-->


#🧠 當執行Bytecode來決定this binding時，會如何決定 ->->-> `會根據是否為箭頭函式來以不同方式來決定。	- 非箭頭函式呼叫，就分別以new binding、implicit binding、explicit binding、default binding來決定他們函式呼叫時的this 是什麼 - 箭頭函式呼叫，就以語彙綁定來決定this是什麼`
<!--SR:!2023-04-20,114,250-->

#🧠 當執行Bytecode來決定this binding時，會如何決定非箭頭函式呼叫 ->->-> `就分別以new binding、implicit binding、explicit binding、default binding來決定他們函式呼叫時的this 是什麼`
<!--SR:!2023-01-28,69,250-->

#🧠 當執行Bytecode來決定this binding時，會如何決定箭頭函式呼叫 ->->-> `箭頭函式呼叫，就以語彙綁定來決定this是什麼`
<!--SR:!2023-01-13,58,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[箭頭函式的this binding是使用語彙綁定(lexical binding)，具體是透過箭頭函式內EC的outer reference往上找上一個EC擁有的this來設定箭頭函式本身的this，且一旦設定，就無法被覆寫]]
[[若一個函式呼叫存在多個this-binding方法的話，那麼this會由誰來決定：explicit binding > implicit binding > default binding 和 new binding > implicit binding > default binding]]
[[new binding 是由new operator 主導來建立一個物件並以此物件作為特定函式呼叫的this]]
[[JS：explicit binding 是相較於implicit binding而言，較為直接且明確告知this是設定什麼]]
[[JS：implicit binding：以暗示的方式來表達this 設定成什麼，losing implicit binding 是指原本會被判定成implicit binding的binding因為特定因素而遺失binding]]
[[JS：default this binding 是指當沒有使用任何一個方法來進行this binding就採用的預設方式]]
References: