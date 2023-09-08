
## 描述

當你想要寫一個middleware能幫忙轉換使用者從http協定轉換成https時，伺服器是以下面形式處理，理論上來說會：
	- 伺服器透過response header來告知客戶端要從http導向至https
	- 寫完header後，就停止後續執行
	- 導向至https
但實際上代碼會是：
	- 伺服器透過 response header來告知客戶端要從http導向至https
	- 寫完header後繼續執行next()
	- 以http來繼續後續請求 (同時間res物件已經寫上新的location)
```
app.use((req, res, next) => {
	if (req.protocol === 'http') {
		res.writeHead(301, { Location: ....})
		res.end()
	}
	return next()
})
```

在實際代碼中並未在寫完後就停止執行，導致後續結果並未如預期般導向，甚至出現錯誤

解法為添加return：
```
app.use((req, res, next) => {
	if (req.protocol === 'http') {
		res.writeHead(301, { Location: ....})
		return res.end()
	}
	return next()
})
```

造成這一切的原因是因爲語法上在理解上會被認為做完就中斷後續執行，比如end就讓人以為執行完就在那停止。

### 其他讓人誤會的語法
1. res.send
2. res.writeHeader
3. res.end
4. res.json
5. res.redirect

## 複習
#🧠 當我們有兩行程式碼，第一行是res.end()，第二行是return next()，請問會如何執行 ->->-> `執行完res.end後，就會執行next()`
<!--SR:!2025-01-27,507,250-->



#🧠 當我們有兩行程式碼，第一行是res.redirect()，第二行是return next()，請問會如何執行 ->->-> `執行完res.redirect後，就會執行next()`
<!--SR:!2023-12-16,99,230-->


#🧠  請問當目前使用者是以http來瀏覽，伺服器會如何執行，會繼續以http?還是以https?其程式碼為如下： ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656511754/blog/middleware/no-return-middleware_ewcc3f.png)->->-> `會先改寫其Header來讓使用者導向至https，然後執行到return next()，接著繼續以http名義後續的請求，並不會中途中斷`
<!--SR:!2023-12-17,100,230-->



#🧠  請問當目前使用者是以http導向至https，如何修改其程式碼使使用者正確以https來發送請求，而不是以http名義來執行![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656511754/blog/middleware/no-return-middleware_ewcc3f.png)->->-> `添加return 至res.end() ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656511754/blog/middleware/with-return-middleware_jnbho6.png)`
<!--SR:!2023-12-18,101,230-->


---
Status: #🌱 
Tags:
[[Express]]
Links:
References:


