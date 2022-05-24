## 描述
讀取指定google storage bucket下的指定物件主要會運用在Google改寫node.js下的stream和file。


讀取檔案可以夾帶著檔案所在的目錄，如xxxxx/xxxx.pem中的xxxxx目錄

- 以指定的file名稱來建立特定file物件，以此來呼叫對應的stream物件來執行讀取，file名稱會是以dir/file的形式，也就是會包含其他名稱，在這裡會是xxxxx/xxxx.pem
```
// 定義bucket 容器上的檔案名稱是叫啥，目前還未上傳至那，即使在這設定，
// 也必須呼叫相關上傳方法才能上傳，並回傳bucket file物件
// 由file 物件來操控著該bucket 容器上的對應檔案(目前還未建立
const blob = bucket.file(filepath)
```

- 設定一個專門讀取指定檔案用的物件，並開始對指定檔案進行下載讀取，其物件會去監測讀取事件
```
const readStream = blob.createReadStream()
```

- 設定readStream讀取回資料的事件-data，將接收到的資料塊chunk組起來來當作chunks的內容
```
.on('data', chunk => { chunks.push(chunk) })	
```

- 設定readStream錯誤事件的處理-error
```
.on('error', (error) => reject(error))
```
- 設定stream接收完資料後所要做的事件處理-end
```
.on('end', () => resolve(chunks))
```


完整程式碼：
```
function readCloudStorageFile(filepath) {
	return new Promise((resolve, reject) => {
		const chunks = []

		const blob = bucket.file(filepath)
		
		const readStream = blob.createReadStream()
		.on('error', (error) => reject(error))
		.on('end', (data) => resolve(chunks))
		.on('data', chunk => {
			chunks.push(chunk)
		})	
	})
}
```

該讀取函式會以陣列來接收每一個stream所拿到的資料，索引位置越前面就代表其資料就於更早的時間接收到，這時只需要concat將他們相連就能得到完整檔案內容：
```
const content = await readCloudStorageFile('xxxxx/xxxx.pem')
const result = Buffer.concat([content[0], content[1]])
```



### readStream的事件
每當資料流下載回部分資料時，就會發送data 事件，接著執行callback
> The 'data' event is emitted whenever the stream is relinquishing ownership of a chunk of data to a consumer
```
on('data', callback)
```
當資料流沒有任何資料時，就發送end事件，接著執行callback
> The `'end'` event is emitted when there is no more data to be consumed from the stream.
```
on('end', callback)
```

當資料流出錯誤時，就發送error事件，接著執行callback
```
on('error', callback)
```

對指定bucket設定acl，只允許擁有者能夠存取

---
Status: #🌱 
Tags:
[[GCP]] - [[JavaScript]]
Links:
References:
[[@node.jsStreamNodeJs]]