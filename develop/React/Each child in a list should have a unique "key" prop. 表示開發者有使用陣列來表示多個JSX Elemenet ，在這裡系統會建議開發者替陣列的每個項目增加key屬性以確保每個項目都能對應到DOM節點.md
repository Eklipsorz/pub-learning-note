## 描述

若宿主環境呈現以下訊息：
> Each child in a list should have a unique "key" prop.

表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂以下問題：
- hooks 沒跟著資料一起調整DOM節點
- 每一次資料上的變更都要花O(N)，N是實際DOM的數量

而建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點



## 複習

#🧠 若宿主環境下呈現 **Each child in a list should have a unique "key" prop.** 訊息，請問表示什麼？->->-> `開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂問題，而建議開發者替陣列的每個項目增加key屬性以確保每個項目都能對應到DOM節點`
<!--SR:!2022-09-13,3,250-->

#🧠 若宿主環境下呈現 **Each child in a list should have a unique "key" prop.** 訊息 表示開發者有使用陣列來表示多個JSX Elemenet ，在這裡系統會擔憂以下問題，問題會是什麼？ ->->-> `- hooks 沒跟著資料一起調整DOM節點，- 每一次資料上的變更都要花O(N)，N是實際DOM的數量`
<!--SR:!2022-09-23,10,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[渲染部分{expression}中的expression是指陣列的話，React 會直接將陣列上的每個元素當成react element 來並排當作渲染內容]]
[[React：Keys概念是用特定資料的識別字去對應著特定Virtual DOM節點，以此在變更內容的情況下，好讓React能夠分辨哪個實際DOM節點是隸屬於哪個資料]]
References: