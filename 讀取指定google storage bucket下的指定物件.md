## 描述
讀取指定google storage bucket下的指定物件主要會運用在Google改寫node.js下的stream和file。




讀取檔案可以夾帶著檔案所在的目錄，如xxxxx/xxxx.pem中的xxxxx目錄


```
// 定義bucket 容器上的檔案名稱是叫啥，目前還未上傳至那，即使在這設定，
// 也必須呼叫相關上傳方法才能上傳，並回傳bucket file物件
// 由file 物件來操控著該bucket 容器上的對應檔案(目前還未建立
const blob = bucket.file(filepath)
```

- 設定一個專門讀取指定檔案用的物件，其物件會去監測
```

```




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

async function main() {
	const content = await readCloudStorageFile('xxxxx/xxxx.pem')
	const result = Buffer.concat([content[0], content[1]])
	console.log(content, result)

}
```



### readStream的事件

```
on('data')
```

```
on('end')
```

```
on('error')
```

對指定bucket設定acl，只允許擁有者能夠存取

---
Status: #🌱 
Tags:
[[GCP]]
Links:
References:



