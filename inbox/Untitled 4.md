## 描述
> ### **04、new 綁定**

> 準確來說，js 中的構造函數只是使用 new 調用的普通函數，它並不是一個類，最終返回的對象也不是一個實例，只是爲了便於理解習慣這麼說罷了。

> 那麼 new 一個函數究竟發生了什麼呢，大致分爲三步：

> 1.  創建一份新空白物件；
> 2.  將新建構的物件設定為那個函式呼叫的this binding
> 3.  將 this和調用參數傳給構造器將空白物件擁有的屬性、方法進行填充；
   4.  若構造器沒有手動返回對象，則回傳目前物件
    

> 這個過程我們稱之爲構造調用，我們來看個例子：

```
function Fn(){
    this.name = '聽風是風';
};
let echo = new Fn();
echo.name//聽風是風
```

> 在上方代碼中，構造調用創建了一個新對象 echo，而在函數體內，this 將指向新對象 echo 上（可以抽象理解爲新對象就是 this）。

> 若對於 new 具體過程有疑惑，或者不知道怎麼手動實現一個 new 方法，可以閱讀博主這篇文章 js new 一個對象的過程，實現一個簡單的 new 方法


> 什麼是建構器(constructor) 。在JS中，建構器只是前面接著new operator被呼叫的函式，他們並沒被接附到類別上，也不會實體化一個類別。他們甚至不是一種特殊的函式。他們只是正規的函式，但調用時，其行為實質上是被前面的new所掌管

> 在函式前面添加new關鍵來呼叫函式，會從函式呼叫轉換成建構式呼叫(constructor call)：
	- 實際上並沒有constructor function，只有函式的建構呼叫(constructor call)

具體的建構呼叫會是以下流程
> 1.  創建一份新空白物件；（即為建構 constructor）
> 2.  設定該物件的protype
> 3.  將新建構的物件設定為那個建構式呼叫的this
> 4.  執行建構式好讓this和相對應物件屬性都建立好
   4.  若構造器沒有手動返回對象，則回傳目前物件


重點：
- function 會是指特定函式，function()為特定函式的呼叫，若前面添加new這operator就是從函式呼叫轉換成建構式呼叫(constructor call) 或者 constructor 就是 new operator + function call 
- constructor call 主要會建構一個擁有特定方法和屬性的物件並回傳，而function則是具體定義物件會有什麼樣屬性和方法
- 具體建構呼叫會是以下流程：
	- 建立一個新空白物件
	- 設定該物件的protype屬性
	- 將新空白物件設定成function呼叫的this
	- 執行function好讓this和參數設定對應物件
	- 若constructor 沒有手動回傳物件，則自動回傳目前設定好的物件
- 細節：
	- 實際上是不存在constructor function，只有從函式呼叫轉換而來的建構式呼叫
- 在這裡this binding 由於會由new operator來主導，所以被稱之為new binding


#### 案例

```
function Fn(){
    this.name = '聽風是風';
};
let echo = new Fn();
echo.name
```

```
function Fn(){
    this.name = '聽風是風';
};
let echo = new Fn();
echo.name//聽風是風
```


## 複習

#🧠 new binding 是什麼樣的binding ->->-> `由`

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``




---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@readfogZhongJavaScriptDeBangDing]]