## 描述
multer 是一個套件，專門解析multipart中的form-data格式，並將解析結果分成圖片和文字，文字就以req.body來回傳，圖片則另外考量到圖片是單個還是多個，若是單個就以req.file來表示，若是多個就以req.files來表示

若沒載入的話，express框架是無法解析multipart/form-data格式。

### multipart/form-data
1. multipart/form-data本身是前端中的表格資料傳遞形式
2. 背景：過去表格的資料傳遞形式只能固定統一皆為文字或者皆為圖片
3. 基於上述背景，才提出multipart/form-data來傳遞擁有文字和圖片的表格
4. 表格如何設定成multipart/form-data？
	- 在表格元件上加入enctype屬性來設定

```
// 建立頁面表單
<form action="/admin/restaurants" method="POST" enctype="multipart/form-data">
```


```
// 編輯頁面表單
<form action="/admin/restaurants/{{restaurant.id}}?_method=PUT" method="POST" enctype="multipart/form-data">
```
## 複習
#🧠 multipart/form-data 是什麼樣的格式 ->->-> `本身是前端中的表格資料傳遞形式，可以從前端傳遞擁有文字和圖片的表格資料至後端`
<!--SR:!2024-04-10,395,250-->
#🧠 multipart/form-data  提出背景為？->->-> `背景：過去表格的資料傳遞形式只能固定統一皆為文字或者皆為圖片`
<!--SR:!2024-05-04,411,250-->

#🧠 前端表格如何設定成multipart/form-data？ ->->-> `在表格元件上加入enctype屬性來設定，如<form action="/admin/restaurants" method="POST" enctype="multipart/form-data">`
<!--SR:!2024-09-06,489,250-->

#🧠 express框架 本身能夠解析multipart/form-data格式嗎 ->->-> `不能解析，需要載入專門解析其格式的套件，如multer`
<!--SR:!2023-10-19,27,190-->

#🧠 multer 是什麼套件？ 以及如何把解析結果傳遞給每個middleware->->-> `multer 是一個套件，專門解析multipart中的form-data格式，並將解析結果分成圖片和文字，文字就以req.body來回傳，圖片則另外考量到圖片是單個還是多個，若是單個就以req.file來表示，若是多個就以req.files來表示`
<!--SR:!2025-01-13,530,230-->

---
Status: #🌱 
Tags:
[[JavaScript]] - [[Express]]
Links:
References:
[[@npmMulter]]