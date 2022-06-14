## 補充知識：Lexical Scope vs. Scope

1. Scope指的是定義某識別字(identifier)對應特定實體的合法使用範圍，在JavaScript中，特定實體會是指變數、函式等，而實現Scope概念的方式具體有Static Scope和Dynamic Scope。

2. 根據前面描述，Scope是一個概念，而Lexical Scope實現該概念的方法之一

3. Static Scope/Lexical Scope 則是在執行之前，先行對原始碼進行文字上的解析，會依據原始碼中變數位置和函式位置來定義以下事情：
 	-  識別字對應的實體是為何
 	-  合法使用的範圍是是什麼
 	-  對應實體的記憶體位置什麼？
 在這Javascript 與大多數的語言多採用靜態範疇，而JavaScript本身也能採用動態範疇，只是通常場景上會採取靜態範疇

4. Dynamic Scope，則是在執行過程來決定每個識別字對應的實體是什麼以及合法使用的範圍是什麼、對應實體的記憶體位置是什麼

  
 
### 補充知識：Lexical Environment vs. Lexical Scope

1. Lexical Environment 和 Lexical Scope 之間最大的差異，就是 Lexical Environment 是在程式執行中存放環境資訊的地方，而 Lexical Scope 則為在程式編譯時就已經決定好的作用域-每個識別字對應特定實體的合法使用範圍


## 複習
#🧠 JavaScript 的Scope是什麼意思？ 具體實現方式有哪些？ ->->-> `Scope指的是定義某識別字(identifier)對應特定實體的合法使用範圍，在JavaScript中，特定實體會是指變數、函式等，而實現Scope概念的方式具體有Static Scope和Dynamic Scope。`


#🧠 JavaScript：Static Scope 和 Lexical Scope差別是？ ->->-> `都是一樣，Static Scope/Lexical Scope 則是在執行之前，先行對原始碼進行文字上的解析，會依據原始碼中變數位置和函式位置來定義識別字對應的實體是為何以及合法使用的範圍是是什麼`


#🧠 JavaScript：Dynamic Scope是什麼？->->-> `在執行過程來決定每個識別字對應的物件是什麼、合法範圍是什麼、記憶體位置在哪`

#🧠 JavaScript：Static Scope 和 Dynamic Scope差別是？ ->->-> `一個是在執行之前就決定每個識別字對應的物件是什麼、合法範圍是什麼、記憶體位置在哪，後者則是在執行過程決定這些`

#🧠 Lexical Environment vs. Lexical Scope 差別是什麼 ->->-> `就是 Lexical Environment 是在程式執行中存放環境資訊的地方，而 Lexical Scope 則為在程式編譯時就已經決定好的作用域-每個識別字對應特定實體的合法使用範圍`

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References: