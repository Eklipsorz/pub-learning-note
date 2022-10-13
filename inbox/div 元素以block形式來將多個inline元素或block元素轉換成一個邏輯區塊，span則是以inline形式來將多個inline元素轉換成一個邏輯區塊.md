## 描述



[[@wikidataSpanYudiv2022]]
> 在HTML中，span與div元素被用來表達一個邏輯區塊。div在Dreamweaver也叫「層」，用於標示塊級元素，而span標示行內元素。

> 絕大多數HTML元素具有語意上的意義 - 也就是說，這個元素表示了它的作用。例如，一個p元素應該包含一段文字，而一個h1元素應該包含頁面的最高層級標題，可據此區分它們。但span和div沒有天生的語意含義，它們可以被用於指定特定的區塊或行列。

> div就像一個段落，在視覺上於頁面隔離出了文件的一部分，它可以包含段落、標題、表格等。span元素的作用是選擇特定文字，以便於指定特殊樣式。



重點：
- div 元素 和 span 元素本身無語意上的意義、無預設事件處理、無預設樣式
- span 元素主要是以inline形式來包含多個inline元素為一個群組或者一個邏輯區塊
- div 元素主要是以block形式來包含多個inline或者block元素為一個群組或者一個邏輯區域

### div 命名緣由
[[@HTMLStandarda]]
> The div element has no special meaning at all. It represents its children

[[@jristaWhatHTMLTag]]
> Division. The DIV tag is is designed to allow you to define **_"divisions"_** of a page (or to "**_divide_** a page into logical containers").

division
>  the process or result of dividing into separate parts; the process or result of dividing something or sharing it out

重點：
- div 元素源自於division名詞
- division 是只將特定事物分割成不同部分的結果或者過程，換言之，被分割出來的部分可以被稱之為division。
- div 本身定義為以block形式來將多個block或者inline元素進行分群


### span 命名緣由
[[@zessxAnswerWhyDiv2015]]
> `<span>` simply comes from the related verb.  
The physically written `<span>` and `</span>` tags span their content. One before, one after. They do nothing more, have no semantic use, no meaning, and are generics, which could explain such a name. For another example, it could have been `<encompass>`.



span
> The span of something that extends or is [spread](https://www.collinsdictionary.com/dictionary/english/spread "Definition of spread") out [sideways](https://www.collinsdictionary.com/dictionary/english/sideways "Definition of sideways") is the [total](https://www.collinsdictionary.com/dictionary/english/total "Definition of total") width of it from one end to the other.

span 
> If something spans a range of things, all those things are included in it.

重點：
- span：以橫向或者單一方向的形式來包含內容
- span 元素源自於span名詞和動詞背後的含義，本身定義為以inline形式來將多個inline元素進行分群


## 複習

#🧠 div 命名緣由為何？ ->->-> `源自於division`
<!--SR:!2022-11-10,28,250-->

#🧠 div 命名源自於division，請問division是什麼意思？ ->->-> `是只將特定事物分割成不同部分的結果或者過程，換言之，被分割出來的部分可以被稱之為division。`
<!--SR:!2022-10-13,10,250-->

#🧠 span 命名緣由為何？->->-> `源自於其span的動詞和名詞，以橫向或者單一方向的形式來包含內容`
<!--SR:!2022-11-10,28,250-->

#🧠 div 元素 和 其他語意化元素相比，有什麼差別->->-> `div元素並不代表著任何語意、沒有事件預設處理、沒有預設樣式`
<!--SR:!2022-11-10,28,250-->

#🧠 span 元素 和 其他語意化元素相比，有什麼差別 ->->-> `span元素並不代表著任何語意、沒有事件預設處理、沒有預設樣式`
<!--SR:!2022-11-10,28,250-->


#🧠 div 元素 最主要的出現理由是因為？ ->->-> `用途，為了以block形式來包含多個inline或者block元素為一個群組或者一個邏輯區域`
<!--SR:!2022-11-10,28,250-->

 #🧠 span 元素 最主要的出現理由是因為？->->-> `span 元素主要是以inline形式來包含多個inline元素為一個群組或者一個邏輯區塊`
<!--SR:!2022-11-10,28,250-->

---
Status: #🌱 
Tags:
[[HTML]]
Links:
References:
[[@HTMLStandarda]]
[[@wikidataSpanYudiv2022]]
[[@jristaWhatHTMLTag]]
[[@zessxAnswerWhyDiv2015]]