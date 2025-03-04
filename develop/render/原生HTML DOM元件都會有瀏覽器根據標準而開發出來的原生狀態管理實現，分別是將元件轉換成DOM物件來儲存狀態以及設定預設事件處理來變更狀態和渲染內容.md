
## 描述


每一個元件下都會有瀏覽器根據標準而開發管理狀態實現，具體是
- 儲存狀態：將元件解析成DOM物件，並將狀態值納入至DOM物件中的屬性
- 更新狀態&根據狀態渲染：
	- 從對應DOM物件上的屬性更改值，就能間接觸發更新狀態和渲染，如對著輸入欄位的value設定為''，就能立即刷新該輸入欄目前顯示的內容
	- 設定預設事件處理來接收狀態並更新DOM物件上的屬性，接著重新渲染一次同個元件


### 案例1：input 元件

假設有一個input元件，瀏覽器根據標準為該元件開發出儲存狀態和根據狀態渲染，分別將狀態轉換成DOM物件的屬性值和設定事件處理


當使用者對著input元件輸入字元時，就會發生change事件，隨之就會觸發瀏覽器的預設事件處理來將接收到的狀態-字元以DOM物件的屬性值來儲存以及渲染目前內容至輸入欄位。


### 案例2： input元件

假設有一個input元件，瀏覽器根據標準為該元件開發出儲存狀態和根據狀態渲染，分別將狀態轉換成DOM物件的屬性值和設定事件處理

當對著input元件的實際DOM節點上的value屬性更動成value1，就會間接觸發其元件的狀態更新和畫面渲染-讓input元件上顯示value1

## 複習

#🧠 元件上都會關注著狀態的什麼 ->->-> `儲存狀態、更新狀態&根據狀態渲染`
<!--SR:!2025-03-13,567,250-->

#🧠 每一個元件下都會有瀏覽器根據標準而開發管理狀態實現，具體是什麼？ ->->-> `- 儲存狀態：將元件解析成DOM物件，並將狀態值納入至DOM物件中的屬性 - 更新狀態&根據狀態渲染： - 從對應DOM物件上的屬性更改值，就能間接觸發更新狀態和渲染，如對著輸入欄位的value設定為''，就能立即刷新該輸入欄目前顯示的內容 - 設定預設事件處理來接收狀態並更新DOM物件上的屬性，接著重新渲染一次同個元件`
<!--SR:!2024-03-11,252,228-->


#🧠 以input元件為例子，請說明發生change事件會是如何以原生DOM結構來實現狀態管理？ ->->-> `假設有一個input元件，瀏覽器根據標準為該元件開發出儲存狀態和根據狀態渲染，分別將狀態轉換成DOM物件的屬性值和設定事件處理。當使用者對著input元件輸入字元時，就會發生change事件，隨之就會觸發瀏覽器的預設事件處理來將接收到的狀態-字元以DOM物件的屬性值來儲存以及渲染目前內容至輸入欄位。
<!--SR:!2024-11-19,452,230-->

#🧠 以input元件為例子，請說明發生當元件的DOM節點之value屬性更動成value1，會發生什麼？ ->->-> `就會間接觸發其元件的狀態更新和畫面渲染-讓input元件上顯示value1`
<!--SR:!2023-11-15,257,248-->
`

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: