


當createClient 帶有legacyMode參數時，只允許以下連線和斷線語法
- connect
- disconnect


當createClient 帶有legacyMode參數時，出現：
- connnect
- quit

會報錯

```
(async function main() {
	const redis = require('redis')
	const NODE_ENV = process.env.NODE_ENV || 'development'
	const redisConfig = require('../config/redis')[NODE_ENV]
	const redisClient = redis.createClient({ url: 'redis://localhost:6379', legacyMode: true })
	// console.log(redisClient)
	// const redisClient = redis.createClient({ url: 'redis://localhost:6379' })

	await redisClient.connect()
	await redisClient.quit()
	//await redisClient.disconnect()
})()
```