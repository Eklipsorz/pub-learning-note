## 描述

若宿主環境呈現以下訊息：
> Each child in a list should have a unique "key" prop.

表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂以下問題：
- hooks 沒跟著資料一起調整DOM節點
- 每一次資料上的變更都要花O(N)，N是實際DOM的數量

而建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點



## 複習

#🧠 在React上使用存有多個JSX元件資訊之陣列來表示特定元件，且不使用keys的話，資料和Virtual DOM之間的關係為何?  為甚麼?->->-> `兩者互為沒關係，因為沒做綁定`
<!--SR:!2023-08-21,2,249-->


#🧠 在React上使用存有多個JSX元件資訊之陣列來表示特定元件，且使用keys的話，資料和Virtual DOM之間的關係為何?  為甚麼?->->-> `資料會對Virtual DOM有綁定關係`
<!--SR:!2023-08-21,2,249-->

#🧠 在React上使用存有多個JSX元件資訊之陣列來表示特定元件，React會先如何表示其元件，請按順序來說，假使沒使用keys ->->-> `先按照陣列大小來分配指定數量的Virtual DOM，並且依序遍歷清單上的每個元素來將資訊寫入至Virtual DOM，寫完一個就寫下一個Virtual DOM，直到遍歷完清單和Virtaul DOM`
<!--SR:!2023-08-21,2,249-->


#🧠 在React上使用存有多個JSX元件資訊之陣列來表示特定元件，React會先如何表示其元件，請按順序來說，假使使用keys ->->-> `先按照陣列大小來分配指定數量的Virtual DOM，並且依序遍歷清單上的每個元素來將資訊寫入至Virtual DOM，寫完一個就綁定其識別字，接著寫下一個Virtual DOM和綁定，直到遍歷完清單和Virtaul DOM`
<!--SR:!2023-09-25,21,249-->


#🧠 若宿主環境下呈現 **Each child in a list should have a unique "key" prop.** 訊息，請問表示什麼？->->-> `開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂問題，而建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點`
<!--SR:!2023-08-21,2,249-->

#🧠 若宿主環境下呈現 **Each child in a list should have a unique "key" prop.** 訊息 表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂以下問題，問題會是什麼？ ->->-> `- hooks 沒跟著資料一起調整DOM節點，- 每一次資料上的變更都要花O(N)，N是實際DOM的數量`
<!--SR:!2023-08-29,2,229-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[渲染部分{expression}中的expression是指陣列的話，React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容]]
[[React：Keys概念是用特定資料的識別字去對應著特定Virtual DOM節點，以此在變更內容的情況下，好讓React能夠分辨哪個實際DOM節點是隸屬於哪個資料]]
References: