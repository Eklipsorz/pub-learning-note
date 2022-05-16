

## 描述
  

### 設定multer 將上傳檔案放置伺服器的記憶體
當伺服器接收到上傳檔案的請求，會於記憶體內建立一個Node.js Buffer 類別的物件來慢慢接收其檔案內容，接著再建立一個file物件，以物件的buffer屬性來指向Buffer 類別的物件

```
static getMulter() {
	const upload = multer({
		storage: multer.memoryStorage(),
		limits: {
			fileSize: MAXFILESIZE
		}
	})
	return upload
}
```

接著當伺服器完成在記憶體儲存上傳檔案的內容時，隨後就會呼叫fileUpload來將檔案上傳至GCP中的Cloud Storage

其背後技術參考於：
	- [[multer： 以硬碟來儲存被上傳的檔案 vs 以記憶體來儲存被上傳的檔案]]
	- [[Node.js Buffer 是為JS提供能夠處理二進制資料的API]]
	- [[Blob 在JavaScript 中是一個專門處理和儲存二進制檔案內容的物件]]

### 將記憶體的檔案上傳至GCP的Cloud Storage
鑑於[[Cloud Storage 是Google 用來儲存資料的雲端服務]]所提供的上傳服務

建立 可操控bucket 容器的 bucket 物件
- 首先建立能與Cloud Storage上的Bucket容器進行連接的bucket物件[[Cloud Storage 是Google 用來儲存資料的雲端服務]]
- 以後只需要向bucket 物件呼叫特定方法就即可操控對應Bucket 容器
```
// PROD_GCLOUD_STORAGE_BUCKET 指定要連接的Bucket 容器名稱
// storage.bucket會回傳能操控對應容器的物件
const bucket = storage.bucket(PROD_GCLOUD_STORAGE_BUCKET)
```


建立bucket file物件，該file物件是由Google 官方定義的類別，
```
// 定義bucket 容器上的檔案名稱是叫啥，目前還未上傳至那，即使在這設定，
// 也必須呼叫相關上傳方法才能上傳，並回傳bucket file物件
// 由file 物件來操控著該bucket 容器上的對應檔案(目前還未建立)
const blob = bucket.file(file.originalname)
```

在本地端(伺服器)與遠端bucket容器上的file物件 兩者間 建立專門 **可寫入的Stream**，該Stream會覆寫bucket 容器上的file 物件所儲存的內容:
	- resumable：true / false ，設定一旦寫入過程發生意外中斷，是否以中斷前的上傳進度來恢復原有進度，若為true，就以中斷前的上傳進度為主；若為false，就會重新上傳
	- 在這裡的resumable 會是false是因為一旦為true，就等同要求Cloud Storage邊上傳指定地點邊上傳另外一個地點，而這地點會是$HOME所指定的位置，通常那個位置是不允許寫入，因此在這為false
	- createWriteStream 會回傳WritableStream型別的物件來操控對應可寫入Stream(包含開始上傳、停止上傳、設定發生問題的事件處理、設定完成寫入的事件處理)

```
const blobStream = blob.createWriteStream({ resumable: false })
```

設定寫入Stream發生問題要如何做：在這裡是直接回傳錯誤物件

```
blobStream.on('error', err => reject(err))
```
設定寫入Stream完成後要如何做：在這裡是回傳檔案上傳至bucket容器後的實際URI位置
```
blobStream.on('finish', () => {
	const dirname = bucket.name
	const filename = encodeURI(blob.name)
			
	const publicURL = format(
		`https://storage.googleapis.com/${dirname}/${filename}`
	)
	return resolve(publicURL)
})
```
實際寫入檔案內容至
	- writestream.end(chunk)：指定內容作為Stream結束寫入前的最後寫入內容，其中chunk會是對應原本內容的二進制資料。
> Calling the writable.end() method signals that no more data will be written to the Writable. The optional chunk and encoding arguments allow one final additional chunk of data to be written immediately before closing the stream.
	- 這裡chunk 會是指定file.buffer，而buffer正是要被上傳的檔案內容(二進制表示)

```
blobStream.end(file.buffer)
```


完整程式碼如下：
```
const bucket = storage.bucket(PROD_GCLOUD_STORAGE_BUCKET)
static cloudStorageHandler(file) {

	return new Promise((resolve, reject) => {

		const blob = bucket.file(file.originalname)
		const blobStream = blob.createWriteStream({ resumable: false })
		blobStream.on('error', err => reject(err))
		blobStream.on('finish', () => {
			const dirname = bucket.name
			const filename = encodeURI(blob.name)
			
			const publicURL = format(
			`https://storage.googleapis.com/${dirname}/${filename}`
			)
			return resolve(publicURL)
		})
		blobStream.end(file.buffer)
	})
}

static async fileUpload(file) {
	try {
		const resultURL = await this.cloudStorageHandler(file)
		return resultURL
	} catch (_) {
		return DEFAULT_AVATAR
	}
}
```



---
Status: #🌱 
Tags:
[[JavaScript]] 
Links:
[[Cloud Storage 是Google 用來儲存資料的雲端服務]]
[[multer： 以硬碟來儲存被上傳的檔案 vs 以記憶體來儲存被上傳的檔案]]
[[Node.js Buffer 是為JS提供能夠處理二進制資料的API]]
[[Blob 在JavaScript 中是一個專門處理和儲存二進制檔案內容的物件]]
References:
[[@GlobalDocumentation]]
[[@huangNodeJsBuffer]]
[[@node.jsHowUseBuffers]]
[[@ReadableStreamWebAPIs]]