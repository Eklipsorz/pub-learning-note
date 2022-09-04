
## 描述

### multer 使用本地端硬碟空間來(暫時)儲存被上傳的檔案


```
const multer = require('multer')
const upload = multer({ dest: 'temp/' })
module.exports = upload
```

multer 會先在硬碟儲存檔案內容，接著建立一個file物件來儲存檔案資訊(位置、大小、檔案名稱)來供使用者能透過該物件來間接存取該檔案，但file物件本身不包含著檔案內容

```
const { files } = req
console.log('files: ', files)

// result: 
files:  [Object: null prototype] {
  avatar: [
    {
      fieldname: 'avatar',
      originalname: '*\x16 2022-04-03 \x0BH5.16.08.png',
      encoding: '7bit',
      mimetype: 'image/png',
      destination: 'temp/',
      filename: 'b8fea83cb632f86e76111de8b3244714',
      path: 'temp/b8fea83cb632f86e76111de8b3244714',
      size: 117354
    }
  ],
  cover: [
    {
      fieldname: 'cover',
      originalname: '*\x16 2022-04-23 \nH1.36.22.png',
      encoding: '7bit',
      mimetype: 'image/png',
      destination: 'temp/',
      filename: 'c169d619fb636792d4de018995d886d3',
      path: 'temp/c169d619fb636792d4de018995d886d3',
      size: 224301
    }
  ]
}

```


### multer 使用本地記憶體來(暫時)儲存被上傳的檔案


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

multer 會先於記憶體建立一個Node.js Buffer[[Node.js Buffer 是為JS提供能夠處理二進制資料的API]]類別的物件來儲存檔案的二進制內容，接著再建立對應file 物件並成為它屬性-buffer
```
console.log('file: ', file, file.buffer instanceof Buffer)
// result:  
file:  {
  fieldname: 'avatar',
  originalname: '*\x16 2022-04-06 \x0BH7.44.32.png',
  encoding: '7bit',
  mimetype: 'image/png',
  buffer: <Buffer 89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52 00 00 01 1a 00 00 00 f2 08 06 00 00 00 92 d3 0a e1 00 00 0c 6a 69 43 43 50 49 43 43 20 50 72 6f 66 69 ... 98994 more bytes>,
  size: 99044
} true

```

## 兩者差別
1. 放在硬碟的話，會以file物件來單純儲存(被上傳)檔案的檔案資訊；放在記憶體的話，會於記憶體構成buffer物件來儲存檔案內容，接著再建立file物件，並以屬性去指向該buffer。
2. 放在硬碟的話，其file物件並不能夠直接讀取該檔案內容，只能以中間人的身份去存取；放在記憶體的話，其file物件能夠透過buffer直接讀取檔案內容。


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[Node.js Buffer 是為JS提供能夠處理二進制資料的API]]
References:
