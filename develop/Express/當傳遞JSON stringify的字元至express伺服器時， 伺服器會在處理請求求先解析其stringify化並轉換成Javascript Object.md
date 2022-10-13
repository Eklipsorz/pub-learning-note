

## 描述
當傳遞JSON stringify的字元至express伺服器時， 伺服器會在處理請求求先解析其stringify化並轉換成Javascript Object

```
{
	"striptToken": "1234",
	"items": [{"id":"5","quantity":"1"},{"id":"6","quantity":"10"}]
}
```


```
req.body = {

	stripeToken: "1234",
	items: [
		{
			id: "5",
			quantity: "1"
		},
		{
			id: "6",
			quantity: "10"
		}
	]

}
```

## 複習
#🧠 當客戶端傳遞JSON stringify內容格式時，伺服器會一接收就解析嗎？其stringify內容會被轉換成物件嗎？->->-> `會`
<!--SR:!2023-03-15,153,250-->

---
Status: #🌱 
Tags:
[[JSON]]
Links:
[[JSON 語法本身以成為JavaScript 資料表示語法中的子集合為目標而設計的資料表示法]]
References:
