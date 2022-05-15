


使用本地端硬碟空間來(暫時)儲存被上傳的檔案

```
const multer = require('multer')
const upload = multer({ dest: 'temp/' })
module.exports = upload
```


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




使用本地記憶體來(暫時)儲存被上傳的檔案
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