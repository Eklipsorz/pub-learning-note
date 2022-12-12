## 描述


### id

[[@mdnIdHTMLHyperText]]
> # id
> The id global attribute defines an identifier (ID) which must be unique in the whole document. Its purpose is to identify the element when linking (using a fragment identifier), scripting, or styling (with CSS).

重點：
- id 是同一份DOM文件用來識別特定節點的識別字串。
- 細節：
	- 每一個DOM文件只會有一個獨特的id，不會出現兩個以上具有相同id的元件
	- 每個節點的id屬性(attribute)只能夠填寫一個id 或者說 每個節點只允許填寫一個獨特id
- 用途：
	- 在JS中，用來挑選一個特定的DOM節點來處理
	- 在CSS中，用來讓selector來挑選一個特定DOM節點以及指定它會有什麼樣外表

### class

[[@mdnClassHTMLHyperText]]
> # class
> The class global attribute is a space-separated list of the case-sensitive classes of the element. Classes allow CSS and JavaScript to select and access specific elements via the class selectors or functions like the DOM method document.getElementsByClassName.

重點：
- class 是同一份DOM文件用來識別特定節點是屬於哪一類的節點
- 細節：
	- 每一個DOM文件可以擁有多個相同名稱的節點
	- 每一個節點的class屬性(attribute)可以擁有多個class，每個class都用空格區隔，class 可以都一樣，不會有影響
	```
	<tag1 class="class1 class2 class3"></tag1>
	```
- 用途：
	- 替多個DOM節點分類
	- 在JS中，用來挑選多個特定的DOM節點來處理
	- 在CSS中，用來讓selector來挑選多個特定DOM節點以及指定它們有什麼樣外表

## 複習

#🧠 HTML DOM上的 id屬性(attribute)是什麼？ ->->-> `是同一份DOM文件用來識別特定節點的識別字串`
<!--SR:!2023-05-26,165,250-->

#🧠 HTML DOM上的id屬性可以這樣填寫嗎? id="id1 id2" 為什麼？->->-> `不能，每一個節點的id屬性只能填寫一個獨特id`
<!--SR:!2023-03-01,113,250-->

#🧠 在同一份HTML DOM文件中，可以有兩個相同ID的HTML DOM 嗎？ 為什麼？ ->->-> `不行，每一個DOM文件只會有一個獨特的id，不會出現兩個以上具有相同id的元件`
<!--SR:!2023-05-12,157,250-->

#🧠 HTML DOM上的 id屬性(attribute)用途是什麼 (js、css用途) ->->-> `在JS中，用來挑選一個特定的DOM節點來處理、 在CSS中，用來讓selector來挑選一個特定DOM節點以及指定它會有什麼樣外表`
<!--SR:!2023-01-05,64,250-->

#🧠 HTML DOM上的 id屬性(attribute)用途是什麼 ->->-> `在JS中，用來挑選一個特定的DOM節點來處理、 在CSS中，用來讓selector來挑選一個特定DOM節點以及指定它會有什麼樣外表`
<!--SR:!2022-12-25,55,250-->



#🧠 HTML DOM上的 class屬性(attribute)是什麼？ ->->-> `是同一份DOM文件用來識別特定節點是屬於哪一類的節點`
<!--SR:!2023-02-04,94,250-->

#🧠 HTML DOM上的class屬性可以這樣填寫嗎? class="class1 class2" 為什麼？ ->->-> `可以，每一個DOM文件可以擁有多個class名稱的節點`
<!--SR:!2023-04-29,148,250-->

#🧠 HTML DOM上的class="class1 class2"中的class1 和 class2 是否可以一樣？為什麼？ ->->-> `可以，本身並沒限定`
<!--SR:!2023-04-16,139,250-->

#🧠 在同一份HTML DOM文件中，可以有兩個相同class的HTML DOM 嗎？ 為什麼？ ->->-> `可以，每一個DOM文件可以擁有多個相同名稱的節點`
<!--SR:!2022-12-24,74,250-->

#🧠 HTML DOM上的 class屬性(attribute)用途是什麼->->-> `	- 替多個DOM節點分類 - 在JS中，用來挑選多個特定的DOM節點來處理 - 在CSS中，用來讓selector來挑選多個特定DOM節點以及指定它們有什麼樣外表`
<!--SR:!2023-04-01,130,250-->


---
Status: #🌱 
Tags:
[[CSS]] - [[HTML]] - [[Rendering]]
Links:
References:
[[@mdnIdHTMLHyperText]]
[[@mdnClassHTMLHyperText]]