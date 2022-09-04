
## 描述

### 問題描述
當createClient 帶有legacyMode參數時，只允許以下連線和斷線語法
- connect
- disconnect

當createClient 帶有legacyMode參數時，出現：
- connnect
- quit

會報錯

比如說以下方式
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
### 解法為
後來發現node-redis本身擁有相容性問題，且依賴於node-redis的connect-redis以及其套件都因此而受害，後來改採用ioredis來實現
redis client

---
Status: #🌱 
Tags:
[[Redis Client]] - [[Redis]]
Links:
References: