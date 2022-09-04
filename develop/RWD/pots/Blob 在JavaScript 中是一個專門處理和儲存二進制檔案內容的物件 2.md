
## 描述

引用[[@mdnBlobWebAPIs]]所描述的Blob：
> The **Blob** object represents a blob, which is a file-like object of immutable, raw data; they can be read as text or binary data, or converted into a [ReadableStream](https://developer.mozilla.org/en-US/docs/Web/API/ReadableStream) so its methods can be used for processing the data.

> Blobs can represent data that isn't necessarily in a JavaScript-native format. The [`File`](https://developer.mozilla.org/en-US/docs/Web/API/File) interface is based on `Blob`, inheriting blob functionality and expanding it to support files on the user's system.

重點：
- Blob 是一個名為Binary Large Object 的物件
- Blob 物件主要儲存著二進制資料(檔案)內容，內容皆以二進制來顯示
- Blob 物件為immutable object，強調著一旦建立Blob物件，其Blob物件所儲存的資料內容就不可在執行中被任何事物給改變
- Blob 物件所儲存的資料內容不一定會是以JS原生格式。
- File 型別是繼承Blob型別


## Note
1. 不可變物件(immutable object)：原意形容某人事物為不可改變、不會被改變的，而在電腦科學裡，是描述著一個物件一旦被建立之後，其內容就不可以被改變，唯讀不可寫；
> immutable: **not changing, or unable to be changed**
> **不可變物件**（英語：Immutable object）是一種物件，在被創造之後，它的狀態（成員變數、屬性等的值）就不可以被改變。至於狀態可以被改變的物件，則被稱為可變物件（mutable object）。


2.  可變物件(mutable object)：原意形容某人事物是能被改變、會被改變的，在電腦科學裡，相對於immutable object，是描述著一個物件一旦被建立之後，其內容是可被改變的。
> **able or likely to change**


---
Status: #🌱 
Tags:
[[Blob]]
Links:
References:
[[@mdnBlobWebAPIs]]