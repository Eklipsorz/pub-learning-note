

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

### 將記憶體的檔案上傳至GCP的Cloud Storage

- 首先建立能與Cloud Storage上的Bucket容器進行連接的bucket物件[[Cloud Storage 是Google 用來儲存資料的雲端服務]]
```
// PROD_GCLOUD_STORAGE_BUCKET 指定要連接的Bucket 容器名稱
// storage.bucket會回傳能操控對應容器的物件
const bucket = storage.bucket(PROD_GCLOUD_STORAGE_BUCKET)
```




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



writestream.end(chunk)

Chunk => 以什麼做為結尾來寫完內容

Calling the writable.end() method signals that no more data will be written to the Writable. The optional chunk and encoding arguments allow one final additional chunk of data to be written immediately before closing the stream.

  

  

**Binary large object**

1.  將二進位資料儲存為一個單一個體的集合

  

1.  將轉換為二進制的內容以一個物件來表示，換言之，用物件去指向其二進制內容

  

  

純JS可以處理unicode編碼字串，且不太能處理二進制(沒有對應二進制資料型別能夠代表二進制資料)，然而當面對充滿二進制內容的檔案流或者TCP封包時，必須要有辦法能夠解析並處理這些二進制內容

而增加buffer類別，以buffer字面上意思來存放二進制並進而處理。

一個 Buffer類似於一個整數數組，但它對應於V8堆內存之外的一塊原始內存。

  



  

為了能讓JS 處理而定義buffer類別

  

Buffers in Node.js => 代表資料內容，且以原始二進制來表示

  

  

  


  

  

IMGUR_CLIENT_ID = 5bdc8196b8d4cb2

 const blobStream = blob.createWriteStream({

    resumable: false,

  });

 
[https://googleapis.dev/nodejs/storage/latest/global.html#:%7E:text=CreateWriteStreamOptions](https://googleapis.dev/nodejs/storage/latest/global.html#:%7E:text=CreateWriteStreamOptions)

  

resumable upload graph api

借助可续传上传，您可以在数据流因通信故障而中断后，恢复数据传输到 Cloud Storage 的操作。可续传上传的工作原理是发送多个请求，每个请求包含您正在上传的对象的一部分。这与简单上传不同，后者在单个请求中包含对象的所有数据，一旦中途失败，则必须从头开始重新上传。

  


    "status": "success",

    "message": "修改成功",

    "data": {

        "account": "user1",

        "email": "belazyuser+1@gmail.com",

        "nickname": "user1",

        "avatar":"https://storage.googleapis.com/belazy-shop/* 2022-04-27 \u000bH5.26.39.png"

    }
	
---
Status: #📥 
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