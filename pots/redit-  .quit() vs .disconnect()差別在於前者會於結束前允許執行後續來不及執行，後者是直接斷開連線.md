
## 描述


### quit 範例
redit- .quit() vs .disconnect()差別在於前者會於結束前允許執行後續來不及執行，後者是直接斷開連線


> Gracefully close a client's connection to Redis, by sending the [`QUIT`](https://redis.io/commands/quit) command to the server. Before quitting, the client executes any remaining commands in its queue, and will receive replies from Redis for each of them.

client.quit()是請求server斷開對應client的連接。

當server在接收到斷開連線(quit)的請求時，會讓那時還在queue的指令先執行完畢，接著再斷開連線。

範例程式碼：
```
// 在這裡會先收到quit指令，但還有ping和get指令，所以會由於定義上的關係而先讓那些指令執行完畢
// 隨後再來斷開連線
const [ping, get, quit] = await Promise.all([
  client.ping(),
  client.get('key'),
  client.quit()
]); // ['PONG', null, 'OK']

// 最後執行完畢後，就斷開連線
// successfully disconnect
try {
  await client.get('key');
} catch (err) {
  // ClosedClient Error
}
```

### disconnect 範例

> Forcibly close a client's connection to Redis immediately. Calling `disconnect` will not send further pending commands to the Redis server, or wait for or parse outstanding responses.

client.disconnect() 是請求server斷開對應client的連接。

當伺服器接收到該請求時，會立即斷線，並不會像quit那樣等待其他指令來執行


```
await client.disconnect();
```

### disconnect 斷線後的值是否存在
問題disconnect 斷線後的值是否存在？
答案是會存在的，直到記憶體完全被釋放，不管以下狀況，皆能獲取曾在記憶體儲存的值：
- 先關閉主要應用伺服器，再重開應用伺服器
- 先關閉redis 資料庫，再重開該資料庫

範例說明：
- get / 路由會嘗試與redis server連接並建立一筆紀錄為key和value1
- get /get 路由會嘗試與redis server連接並獲取對應key的值
- get /close 路由會嘗試斷線

流程為：
- 先執行get / 來嘗試紀錄key:value1這紀錄
- 接著執行get /close來斷線，實現key:value1是否被釋放
- 最後執行 get /get 來重新獲取對應key值，結果是仍能回傳原先的值-value1



```
app.get('/', async () => {
	console.log('hi')
	await client.connect()
	await client.set('key', 'value1')
	const value = await client.get('key')
	console.log(value)
})

app.get('/get', async () => {
	await client.connect()
	const value = await client.get('key')
	console.log('in get route:', value)
})

app.get('/close', async () => {
	await client.disconnect()
	console.log('disconnected')
})
```


---
Status: #🌱 
Tags:
[[Redis]] - [[NoSQL]]
Links:
[[redis 是將資料存放記憶體的NOSQL資料庫，資料會是以key-value pair的形式]]
[[node.js 透過node-redis程式來與redis server連線並下達對應資料庫指令]]
References:
[[@Redis]]