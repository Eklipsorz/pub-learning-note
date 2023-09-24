## 描述



### form的action屬性和method屬性

> 1. form是由標籤(label)、輸入欄(input)、按鈕(button)所組成，
> 
> 2. action屬性是指定當form發生提交時，指定提交內容要傳到何處，例子：當提交時，可設定action為/action_page.php，這樣它會把資料傳至action_page.php當檔案的參數來處理

```
<form action="/action_page.php" method="get">

	<label for="fname">First name:</label>
	<input type="text" id="fname" name="fname">

	<label for="lname">Last name:</label>
	<input type="text" id="lname" name="lname">

	<input type="submit" value="Submit">
</form>
```

> 3. method 指定何種形式來傳提交方式，有GET和POST


參考資料：
https://www.w3schools.com/tags/att_form_method.asp

> 4. 提交事件的發生會是由form內部具有type=submit屬性值的元件來決定，而通常只要對那個元件進行點擊，就發生submit事件，而當發生事件時，event object指向的target會是整個表單，而非那實際上被點擊的元件。
> 
> 5. 若都正確設定action和method這兩個屬性，會將內容傳遞給指定位置，也就是action所指定的地方，若沒有設定action時，會自動導向回當前頁面

target 屬性
> Indicates where to display the response after submitting the form

[[@w3schoolHTMLFormTarget]]
> The `target` attribute specifies a name or a keyword that indicates where to display the response that is received after submitting the form.
> 
> _self -> The response is displayed in the same frame (this is default)

重點：
- form 表單通常是由標籤(label)、輸入欄(input)、按鈕(button)等元件所構成
- form 表單本身就有預設事件處理，如
	- 提交時的預設事件處理是以表格資料傳遞至指定頁面上，並按照target來將使用者導向至特定位置來顯示接收結果
- form 屬性：
	- method：指定表格資料的傳遞方法，如get、post
		- 預設值為get
	- action：指定表格資料要傳遞的目的頁面，若沒有填寫，會直接以目前頁面來傳遞
		- 預設值為目前頁面
	- target：指定提交表格後要在哪邊呈現接收結果，具體會有指向目前頁面的"\_self"
		- 預設值為"\_self"

#### 預設事件處理
[[@dillionmegidaHowManageBrowser2022]]：
> Browsers have default interactions and behaviors for different events.

重點：
- 預設事件處理是由瀏覽器替特定事件所綁定的事件處理，只要開發者沒特別停止該預設事件，就會以預設的事件處理來處理事件。

#### 使用get 來傳遞表格

> 二、透過 GET 傳遞資料： 雖然GET本身就是讀取，但在這裡是提交表單的方法之一，會將表單內容以key/value pair這個形式放置URL，好讓action能夠透過URL收到資料
```
<form action="接收資料的 PHP 程式" method="get"></form>
```

重點：
- 使用get來傳遞，會將資料表格依照欄位和欄位值來組成多個key-value pairs，然後以URL夾帶這些資料，並傳遞至指定頁面

#### 使用post 來傳遞表格

> 一、透過 POST 傳遞資料： 把表單資料放到http要求封包內部並將此封包傳遞至action所指定的地方。
```
<form action="接收資料的 PHP 程式" method="post"></form>
```

重點：
- 使用post來傳，會將資料表格依照欄位和欄位值來組成多個key-value pairs，然後以封包形式來傳遞至指定頁面。

### 對著表單裡的表格按點擊時

> 提交事件的發生會是由form內部具有type=submit屬性值的元件來決定，而通常只要對那個元件進行點擊，就發生submit事件，而當發生事件時，event object指向的target會是整個表單，而非那實際上被點擊的元件。



```
<form>
	<button type="submit"> Add Expense </button>
</form>
```


重點：
- 當在提交表格上的提交按鈕發生點擊時，會直接觸發form的提交事件



### preventDefault()
> 是event object的方法，用來去掉/避免/預防event object對應元件所要做的預設處理器內容
> 其方法可以任意放在指定事件的位置，可以是第一行

```
element.addListenerEvent(event, function(event) {
	event.preventDefault()
	// do something
})
```
> 也可是放在後頭
```
element.addListenerEvent(event, function(event) {
	// do something
	event.preventDefault()
})
```

> 不論位置如何，只要有放置方法，就會優先去掉/避免/預防預設處理器內容。
>
> 3. 但只是告訴瀏覽器不要做預設的事件處理器內容，不會停止事件傳遞


> Event.stopPropagation()
>
>Event 介面的 stopPropagation() 方法可阻止當前事件繼續進行捕捉（capturing）及冒泡（bubbling）階段的傳遞。

由於執行前會編譯，會預先知道有沒有event.preventDefault()，不論其程式碼位置是否放到最後面，若有就先停止目前元件的預設事件處理來執行：
[[@mdnEventPreventDefaultWeb]]
> Calling `preventDefault()` during any stage of event flow cancels the event, meaning that any default action normally taken by the implementation as a result of the event will not occur.


重點：
- 由於執行前會編譯，會預先知道有沒有event.preventDefault()，不論其程式碼位置是否放到最後面，若有就先停止目前元件的預設事件處理來執行
- preventDefault 本身不會停止事件傳遞，若要停止capturing和bubble這兩種事件傳遞：
	- capturing：從window元件傳遞至form
	- bubble：從form傳遞至window元件
```
event.stopPropagation()
```

## 複習

#🧠 form 表單通常是由什麼元件來構成的？ ->->-> `標籤(label)、輸入欄(input)、按鈕(button)`
<!--SR:!2024-04-04,360,250-->

#🧠  預設事件處理是什麼？ 誰設定？->->-> `由瀏覽器替特定事件所綁定的事件處理，只要開發者沒特別停止該預設事件，就會以預設的事件處理來處理事件。`
<!--SR:!2023-11-09,267,250-->


#🧠 form 本身存在哪些預設事件處理？ 舉例說明 ->->-> `form 發生提交時的預設事件處理`
<!--SR:!2025-03-05,562,250-->


#🧠 form 提交事件是如何觸發？ ->->-> `在表單中的負責提交事件種類按鈕發生點擊時，就會觸發`
<!--SR:!2024-11-06,491,250-->

#🧠 form 提交事件的預設事件處理是什麼？換言之，當發生提交時，會以什麼樣的預設處理來進行？ ->->-> `提交時的預設事件處理是以表格資料傳遞至指定頁面上，並按照target來將使用者導向至特定位置來顯示接收結果`
<!--SR:!2023-11-26,277,250-->

#🧠 form 標籤有哪些常用屬性(attributes) ->->-> `method、action、target`
<!--SR:!2024-08-13,324,230-->

#🧠 form 標籤的method 屬性是做什麼？ 能填寫什麼值->->-> `指定表格資料的傳遞方法，如get、post`
<!--SR:!2024-02-28,332,250-->

#🧠  form 標籤的action屬性是做什麼？->->-> `指定表格資料要傳遞的目的頁面`
<!--SR:!2024-11-01,487,250-->


#🧠 form 標籤的target屬性是做什麼？ ->->-> `指定提交表格後要在哪邊呈現接收結果`
<!--SR:!2024-01-27,315,250-->

#🧠 form 標籤的method 預設屬性值為何 ->->-> `get`
<!--SR:!2023-12-06,107,230-->

#🧠 form 標籤的action 預設屬性值為何 ->->-> `目前頁面`
<!--SR:!2024-04-25,371,250-->


#🧠 form 標籤的target 預設屬性值為何->->-> `具體會有指向目前頁面的"\_self"`
<!--SR:!2024-01-25,282,230-->

#🧠 form 標籤使用method=get來傳遞表格資料，會如何傳遞？->->-> `使用get來傳遞，會將資料表格依照欄位和欄位值來組成多個key-value pairs，然後以URL夾帶這些資料，並傳遞至指定頁面`
<!--SR:!2023-12-11,107,230-->

#🧠 form 標籤使用method=post來傳遞表格資料，會如何傳遞？->->-> `使用post來傳，會將資料表格依照欄位和欄位值來組成多個key-value pairs，然後以封包形式來傳遞至指定頁面。`
<!--SR:!2024-01-25,315,250-->

#🧠 如何撤銷 form 預設提交事件？ ->->-> `使用event.preventDefault()、event.stopPropagation()`
<!--SR:!2023-12-12,109,230-->

#🧠 event.preventDefault() 是做什麼？ ->->-> `撤銷掉目前發生事件的元件所要做的預設事件處理`
<!--SR:!2025-03-11,565,250-->

#🧠 event.preventDefault() 會停止事件訊號傳遞嗎？若沒，該如何改善 ->->-> `並不會停止，若要停止caturing 和 bubble這兩種事件訊號傳遞，可以額外添加event.stopPropagation()`
<!--SR:!2023-12-12,287,250-->

#🧠  event.preventDefault() 放在程式碼後頭能夠先撤銷掉目前預設事件處理嗎 ？->->-> `能，會於執行前會編譯，會預先知道有沒有event.preventDefault()，不論其程式碼位置是否放到最後面，若有就先停止目前元件的預設事件處理來執行`
<!--SR:!2024-01-18,287,249-->


---
Status: #🌱 
Tags:
[[HTML]] - [[Rendering]]
Links:
References:
[[@w3schoolHTMLFormMethod]]
[[@dillionmegidaHowManageBrowser2022]]
[[@w3schoolHTMLFormTarget]]
[[@mdnEventStopPropagationWeb]]
[[@mdnEventPreventDefaultWeb]]