## 描述

[[@hebhJavaScriptBianYiYuanLiYuYuYanJingCuiZhiHu]] 所描述：
> 语法分析

> 接下来语法分析器（Grammar Parser）采用上下文无关语法（Context-free Grammar）之类的分析手段，将这些Token进行语法分析，产生语法树（Syntax Tree）。

> 简单的说，由语法分析器产生的语法树就是以表达式（Expression）为节点的树。


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658414132/blog/javascript/compile/grammar-parser-example_ha2m9e.jpg)

> 接着语义分析器（Semantic Analyzer）完成对表达式的语法层面的分析，但它并不了解这个语句是否有意义（如两个指针相乘无意义，但是这一步检测不出）。

> 编译器所能分析的语义是静态语义（Static Semantic），即在编译期可以确定的语义，通常包括声明和类型的匹配、类型的转换。如C风格的隐式转换这一步都要做好。而像除以0这样的错误则属于动态语义（Dynamic Semantic），在运行期才能确定。

> 经过语义分析后，整个语法树的表达式都被标识了类型，对于那些隐式转换的类型也将会在这一步被插入相应的转换节点：

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1658414132/blog/javascript/compile/semantic-parser-example_obg0xm.jpg)


重點：
- 執行時機點：JavaScript編譯時期中的Parsing
- 執行順序：
	- Gammar Parser -> Semantic Analyer
- Grammar Parser 主要會解析字串是否為程式語言能夠識別的語法以及是否能與其他文字組裝成合法的statement、expression、declaration。
	- 若有問題的話，會報錯。
	- 若成功的話，會組成一顆樹狀結構
- Semantic Analyer：主要解析從Grammar Parser得到的樹狀結構中並試著其結構上的(還未明意思的)文字上意思，在這裏會是補充每個句子中的變數、常數、回傳值的資料型別是什麼？是否為整數、是否為字串、是否為陣列
	- 若有問題的話，會報錯
	- 若成功的話，會以目前的樹狀結構補充資訊，如資料型別資訊

### Gammar 命名緣由

> the rules about how words change their form and combine with other words to make sentences

重點：
- Gammar 是一組定義合法句子的規則
- 主要會將多個文字轉換形式、並與其他文字組合成句子

### Semantic 命名緣由 
> connected with the meanings of words

重點為：
- Semantic是指文字上意思相關的
## 複習
#🧠 Gammar 命名緣由是什麼？ ->->-> `Gammar 是一組定義合法句子的規則，主要會將多個文字轉換形式、並與其他文字組合成句子`
<!--SR:!2022-08-03,10,250-->

#🧠 Semantic 命名緣由是什麼？ ->->-> `Semantic是指文字上意思相關的`
<!--SR:!2022-08-03,10,250-->


#🧠 JavaScript 編譯時期中的Parsing 會是執行什麼？ ->->-> `會先將tokenizing獲取到的token陣列 經過 Grammar Parser 來檢查是否能夠組成合法的statement、expression、declaration，若能的話，就是一個樹狀結構來代表他們，若不能就報錯，最後再經過semantic analyer來解析結構上那些還未明語意的文字是什麼意思，具體會是賦予變數、常數、回傳值、宣告的資料型別是什麼`
<!--SR:!2022-08-03,10,250-->


#🧠 JavaScript 編譯時期中的Grammar Parser 是什麼？ ->->-> `主要會解析字串是否為程式語言能夠識別的語法以及是否能與其他文字組裝成合法的statement、expression、declaration`
<!--SR:!2022-08-01,8,250-->

#🧠 JavaScript 編譯時期中的Grammar Parser 檢測tokenizing 文字，若有問題會是？ ->->-> `若有問題的話，會報錯`
<!--SR:!2022-08-03,10,250-->

#🧠 JavaScript 編譯時期中的Grammar Parser 檢測tokenizing 文字，若沒問題會是？ ->->-> `若成功的話，會組成一顆樹狀結構`
<!--SR:!2022-08-03,10,250-->

#🧠 JavaScript 編譯時期中的Semantic Analyer是什麼？->->-> `主要解析從Grammar Parser得到的樹狀結構中並試著其結構上的(還未明意思的)文字上意思，在這裏會是補充每個句子中的變數、常數、回傳值的資料型別是什麼？是否為整數、是否為字串、是否為陣列`
<!--SR:!2022-08-03,10,250-->

#🧠 經過JavaScript 編譯時期中的Semantic Analyer 處理後，有問題會是？ ->->-> `若有問題的話，會報錯`
<!--SR:!2022-08-03,10,250-->

#🧠 經過JavaScript 編譯時期中的Semantic Analyer 處理，沒問題會是？ ->->-> `若成功的話，會以目前的樹狀結構補充資訊，如資料型別資訊`
<!--SR:!2022-08-03,10,250-->

---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[JavaScript 是一個具有編譯、直譯特性的直譯語言，執行前會先編譯中間碼然後邊解析邊執行]]
[[JavaScript 會在編譯時期分配記憶體給函式宣告、var宣告、定義各種scope的execution context]]
References:
[[@hebhJavaScriptBianYiYuanLiYuYuYanJingCuiZhiHu]]