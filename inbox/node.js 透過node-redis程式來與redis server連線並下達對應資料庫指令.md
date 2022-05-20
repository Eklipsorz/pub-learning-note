
## 描述

引述[[@Redis]]所描述的：
> node-redis is a modern, high performance [Redis](https://redis.io) client for Node.js.

node-redis 是一個能與redis server相連接的redis client程式，並且提供介面給予node.js透過它來與redis server連接

## 安裝
```
npm install redis
```

### 範例
流程：
- 先載入redis套件
```
const redis = require('redis')
```
- 先讓node-redis與redis server進行連接
```
const redisURL = 'redis://localhost:6680'
const client = redis.createClient({ url: redisURL })
```

- 正式連接
```
await client.connect()
```

- 設定key-value pair形式的紀錄
```
await client.set('key', 'value1')
const value = await client.get('key')
```

完整程式碼：
```

const redis = require('redis')
const redisURL = 'redis://localhost:6680'
const client = redis.createClient({ url: redisURL })


const express = require('express')
const app = express()
const port = 3000
  
client.on('error', (err) => console.log('Redis Client Error', err))  

app.get('/', async () => {
	await client.connect()
	await client.set('key', 'value1')
	const value = await client.get('key')
	console.log(value)
})

app.listen(port, () => {
	console.log(`The express server is running at ${port}`)
})
```

---
Status: #🌱 
Tags:
[[Redis]] - [[NoSQL]]
Links:
[[redis 是將資料存放記憶體的NOSQL資料庫，資料會是以key-value pair的形式]]
References:
[[@Redis]]