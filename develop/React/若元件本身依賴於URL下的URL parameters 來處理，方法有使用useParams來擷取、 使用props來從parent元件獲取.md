## 描述


### 若元件本身依賴於URL下的URL parameters 來處理
可以使用以下方式來獲取：
1. 使用useParams來擷取：考量到元件不一定就會在Route內，若貿然添加會使該元件的可重複率變低。
2. 使用props來從parent元件獲取：可提昇可重複使用



## 複習

#🧠 react：若元件本身依賴於URL下的URL parameters 來處理，獲取方式有哪些？ ->->-> ` 使用useParams來擷取、 使用props來從parent元件獲取`
<!--SR:!2024-06-18,336,250-->

#🧠 若元件本身依賴於URL下的URL parameters 來處理，獲取方式有哪些？ ->->-> ` 從宿主環境上取得目前頁面的位址、從client-side router攔截到的請求內容來擷取`
<!--SR:!2024-02-25,225,250-->


#🧠 若元件本身依賴於URL下的URL parameters 來處理，若使用useParams來擷取會有什麼潛在問題->->-> `考量到元件不一定就會在Route內，若貿然添加會使該元件的可重複率變低。`
<!--SR:!2024-01-31,200,230-->

#🧠 若元件本身依賴於URL下的URL parameters 來處理，其中使用useParams的潛在問題會是考量到元件不一定就會在Route內，若貿然添加會使該元件的可重複率變低，會有什麼樣的解法來提昇可重複使用率->->-> ` 使用props來從parent元件獲取`
<!--SR:!2023-09-28,189,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References: