## 描述

當在提交表格上的提交按鈕發生點擊時，會直接觸發form的提交事件

```
<form>
	<button type="submit"> Add Expense </button>
</form>
```


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

> 一、透過 POST 傳遞資料： 把表單資料放到http要求封包內部並將此封包傳遞至action所指定的地方。
```
<form action="接收資料的 PHP 程式" method="post"></form>
```

> 二、透過 GET 傳遞資料： 雖然GET本身就是讀取，但在這裡是提交表單的方法之一，會將表單內容以key/value pair這個形式放置URL，好讓action能夠透過URL收到資料
```
<form action="接收資料的 PHP 程式" method="get"></form>
```

參考資料：
https://www.w3schools.com/tags/att_form_method.asp

> 4. 提交事件的發生會是由form內部具有type=submit屬性值的元件來決定，而通常只要對那個元件進行點擊，就發生submit事件，而當發生事件時，event object指向的target會是整個表單，而非那實際上被點擊的元件。
> 
> 5. 若都正確設定action和method這兩個屬性，會將內容傳遞給指定位置，也就是action所指定的地方，若沒有設定action時，會自動導向回當前頁面

  

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


## 複習



---
Status: 
Tags:
Links:
References: