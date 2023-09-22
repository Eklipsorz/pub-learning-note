## 描述



### duck typing
[[@YaZiXingBieWeiJiBaiKeZiYouDeBaiKeQuanShu]]
> 鴨子型別（英語：duck typing）在程式設計中是動態型別的一種風格。在這種風格中，一個物件有效的語意，不是由繼承自特定的類或實現特定的介面，而是由「當前方法和屬性的集合」決定。這個概念的名字來源於由詹姆斯·惠特科姆·萊利提出的鴨子測試（見下面的「歷史」章節），「鴨子測試」可以這樣表述：

	「當看到一隻鳥走起來像鴨子、游泳起來像鴨子、叫起來也像鴨子，那麼這隻鳥就可以被稱為鴨子。」

> 在鴨子型別中，關注點在於物件的行為，能做什麼；而不是關注物件所屬的類型。例如，在不使用鴨子型別的語言中，我們可以編寫一個函式，它接受一個類型為「鴨子」的物件，並呼叫它的「走」和「叫」方法。


[[@JinYiBuSiKaoDuckTypingIThome]]
> 由於變數本身不帶型態資訊，動態定型語言在設計方法時，想要不受限於物件型態而僅思考物件應當具有的行為，也就是進行所謂Duck typing時，極為容易。

> 然而Duck typing並非動態定型語言專屬，靜態定型語言也能夠進行Duck typing，只不過在方式上通常較動態定型麻煩，既然動態與靜態定型都有能力進行Duck typing，那麼進一步思考兩者間的差異，才能真正發揮與掌握Duck typing。

**你只要像個鴨子呱呱叫**

> 支持者最愛擁抱動態定型語言的理由之一就是，實作Duck typing時極為容易，也就是「當我看到一隻鳥，它走路像鴨子，游泳像鴨子，叫聲像鴨子，我就稱其為鴨子」此說法最初起源，可能來自美國印第安納詩人James Whitcomb Riley，用來表示可觀察未知事物的外在特徵，以推斷該事物的本質，後來在程式設計也常用來隱喻動態定型語言的設計風格，若使用動態定型的Ruby語言來示範，可定義一個doQuack方法：

**def doQuack(duck)  
    duck.quack  
end**

> 參數duck沒有任何型態宣告，也因此，不會有任何型態約束，只要傳進來的物件具有quack方法就可以了，在快速開發、程式規範尚未確立的階段若有新需求，只要在doQuack方法中修改，不用費心地修改類別等定義，這個特性是非常有用的功能，如果語言本身又有支持物件個體化（Object individuation），即使物件原本沒有quack方法，也可以臨時添加再做為引數傳入。例如，Ruby可以臨時為物件定義單例方法（singleton method ），就能滿足呼叫doQuack的需求：

**dog = Dog.new  
def dog.quack  
    print "quack"  
end  
doQuack(dog)**

重點：
- duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格
- 風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別，而不是關注特定事物所屬的類別、介面、原型
- duck typing 原有概念為
	「當看到一隻鳥走起來像鴨子、游泳起來像鴨子、叫起來也像鴨子，那麼這隻鳥就可以被稱為鴨子。」
- duck typing 適用於滿足以下特性的語言
	- dynamic typing
	- static typing

#### type & typing  在電腦科學上的命名緣由

[[@TypeSystemWikipedia]]
> Assigning a data type, termed typing, gives meaning to a sequence of bits such as a value in memory or some object such as a variable. 

重點：
- type 賦予特定資料型別至一組二進制序列、記憶體內容、內容
- typing 則是強調 **賦予型別至特定內容** 的方法或者過程



## 複習

#🧠 type 在電腦科學上的命名緣由為何？以動詞來說->->-> `type 賦予特定資料型別至一組二進制序列、記憶體內容、內容`
<!--SR:!2024-03-04,241,250-->

#🧠 typing  在電腦科學上的命名緣由為何  ->->-> ` typing 則是強調 **賦予型別至特定內容** 的方法或者過程`
<!--SR:!2024-06-08,282,230-->

#🧠 duck typing 是什麼東西？->->-> `duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格`
<!--SR:!2023-11-27,185,250-->

#🧠 duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，其風格主旨為何？->->-> `風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別，而不是關注特定事物所屬的類別、介面、原型`
<!--SR:!2023-12-05,74,190-->

#🧠 duck typing 主要用來決定特定事物是屬於哪一種物件型別的風格，其風格關係什麼以及不關心什麼？->->-> `風格主要是關注特定事物所具有的行為會做什麼，接著依據行為來判別是否為特定物件型別，而不是關注特定事物所屬的類別、介面、原型`
<!--SR:!2024-02-18,233,250-->

#🧠 duck typing 適用於滿足哪些特性的語言 ->->-> `	- dynamic typing - static typing`
<!--SR:!2024-04-12,263,250-->

#🧠 duck typing 典故為何？->->-> `當看到一隻鳥走起來像鴨子、游泳起來像鴨子、叫起來也像鴨子，那麼這隻鳥就可以被稱為鴨子。`
<!--SR:!2024-03-01,241,250-->






---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
References:
[[@TypeSystemWikipedia]]
[[@JinYiBuSiKaoDuckTypingIThome]]
[[@YaZiXingBieWeiJiBaiKeZiYouDeBaiKeQuanShu]]