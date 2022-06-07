

當對req.session的任一屬性進行寫入時，系統就會向redis發送建立對應session來儲存，但一開始沒那麼快建立好session，所以會在下面最後兩行失敗

```
static async getSession(req, _, next) {

	if (req.session && req.session.cartId) {
		return next()
	}

	req.session.cartId = uuidv4()
	req.session.firstSyncBit = false


	const createdAt = new Date()
	const key = `sess:${req.session.id}`
	console.log(key)

	const config = {
		key, createdAt, days: 7
	}



	// req.session.expireAtConfig = config
	// // await RedisToolKit.setExpireAt(config, redisClient)
	// await redisClient.expiredat(key, 1655247298)

	const redisClient = req.app.locals.redisClient
	console.log(await redisClient.get(key))
	console.log(await redisClient.expire(key, 604800))

	return next()

}
```


結果：
```
The express server is running at 3000
sess:NN7tMzIVE1amMCtkm907OOhxoOqd4C6Y
null
0
```