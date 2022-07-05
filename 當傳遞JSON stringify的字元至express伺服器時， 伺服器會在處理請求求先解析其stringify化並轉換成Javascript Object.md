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