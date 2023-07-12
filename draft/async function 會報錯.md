若添加async 在function之前會報錯，錯誤訊息為redisClient.connect is not a function


```
async function createRedisClient({ username, password, host, port }) {
	const url = `redis://${username}:${password}@${host}:${port}`
	const client = redis.createClient({ url })
	client.on('error', (err) => console.log('Redis Client Error: ', err))
	console.log('inside : ', url)
	return client
}

exports = module.exports = createRedisClient
```



```
function createRedisClient({ username, password, host, port }) {
	const url = `redis://${username}:${password}@${host}:${port}`
	const client = redis.createClient({ url })
	client.on('error', (err) => console.log('Redis Client Error: ', err))
	console.log('inside : ', url)
	return client
}

exports = module.exports = createRedisClient
```