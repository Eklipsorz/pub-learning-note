The **Blob** object represents a blob, which is a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) so its methods can be used for processing the data.

  
https://zh.wikipedia.org/zh-tw/不可變物件
  

writestream.end(chunk)

Chunk => 以什麼做為結尾來寫完內容

Calling the writable.end() method signals that no more data will be written to the Writable. The optional chunk and encoding arguments allow one final additional chunk of data to be written immediately before closing the stream.

  

  

**Binary large object**

1.  將二進位資料儲存為一個單一個體的集合

  

1.  將轉換為二進制的內容以一個物件來表示，換言之，用物件去指向其二進制內容

  

  

純JS可以處理unicode編碼字串，且不太能處理二進制(沒有對應二進制資料型別能夠代表二進制資料)，然而當面對充滿二進制內容的檔案流或者TCP封包時，必須要有辦法能夠解析並處理這些二進制內容

而增加buffer類別，以buffer字面上意思來存放二進制並進而處理。

一個 Buffer類似於一個整數數組，但它對應於V8堆內存之外的一塊原始內存。

  

比如一個圖片的buffer會是

<Buffer 89 50 4e 47 0d 0a 1a 0a 00 00 00 0d 49 48 44 52 00 00 02 00 00 00 02 00 08 06 00 00 00 f4 78 d4 fa 00 00 00 04 73 42 49 54 08 08 08 08 7c 08 64 88 00 ... 8567 more bytes>

[https://morosedog.gitlab.io/nodejs-20200123-Nodejs-11/](https://morosedog.gitlab.io/nodejs-20200123-Nodejs-11/)

[https://nodejs.org/en/knowledge/advanced/buffers/how-to-use-buffers/](https://nodejs.org/en/knowledge/advanced/buffers/how-to-use-buffers/)

  

  

為了能讓JS 處理而定義buffer類別

  

Buffers in Node.js => 代表資料內容，且以原始二進制來表示

  

  

  

Pure JavaScript, while great with unicode-encoded strings, does not handle straight binary data very well. This is fine on the browser, where most data is in the form of strings. However, Node.js servers have to also deal with TCP streams and reading and writing to the filesystem, both of which make it necessary to deal with purely binary streams of data.

  

One way to handle this problem is to just use strings anyway, which is exactly what Node.js did at first. However, this approach is extremely problematic to work with; It's slow, makes you work with an API designed for strings and not binary data, and has a tendency to break in strange and mysterious ways.

  

Don't use binary strings. Use buffers instead!

  

  

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
References:
[[@GlobalDocumentation]]
[[@huangNodeJsBuffer]]
[[@node.jsHowUseBuffers]]
[[@ReadableStreamWebAPIs]]