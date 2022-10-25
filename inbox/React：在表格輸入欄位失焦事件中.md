
## 描述



### onblur 事件處理主要負責

- 設定touched
- 內容驗證



### onblur

> The onblur event occurs when an object loses focus.

重點：
- onblur 是指當特定事物與周遭事物之間是沒差異時的事件處理屬性，具體特定事物和周遭事物之間沒差異是指特定事物和周遭事物都會是inactive element，只是特定事物剛從active element轉移至inactive element
- blur 是相對於DOM節點之focus的概念：
	- focus會是將特定元件標記成active element
	- blur則是從active element轉移至inactive element


#### React 體系是使用onBlur，屬性值是函式物件

### blur 命名緣由


> to make the difference between two things less clear, or to make it difficult to see the exact truth about something

重點：
- blur 意指為使特定事物與周遭事物之間差異沒有差異或者難以看出特定事物和周遭事物之間的差異

## 複習

#🧠 blur 作為動詞的命名緣由 ->->-> `意指為使特定事物與周遭事物之間差異沒有差異或者難以看出特定事物和周遭事物之間的差異`
<!--SR:!2022-11-01,7,250-->

#🧠 HTML 標籤上的onblur 屬性是什麼？ ->->-> `onblur 是專門指定當特定事物與周遭事物之間是沒差異時所要做的指令`
<!--SR:!2022-11-03,9,250-->

#🧠 HTML 標籤上的onblur 屬性 是專門指定當特定事物與周遭事物之間是沒差異時所要做的指令，那麼何謂沒差異？？？->->-> `具體特定事物和周遭事物之間沒差異是指特定事物和周遭事物都會是inactive element，只是特定事物剛從active element轉移至inactive element`
<!--SR:!2022-11-04,10,250-->

#🧠 blur 是相對於DOM節點之focus的概念，focus會是指什麼？blur又是指什麼？ ->->-> `	- focus會是將特定元件標記成active element - blur則是從active element轉移至inactive element`
<!--SR:!2022-11-04,10,250-->

#🧠 onblur 事件處理主要負責什麼業務？->->-> `設定touched/untouched狀態、內容驗證`
<!--SR:!2022-10-27,2,230-->

#🧠 HTML 標籤上下的onblur 在React對應的標籤屬性是什麼？屬性值又是如何？->->-> `onBlur，其屬性值會是函式物件`
<!--SR:!2022-11-04,10,250-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
References: