

> Pure JavaScript, while great with unicode-encoded strings, does not handle straight binary data very well. This is fine on the browser, where most data is in the form of strings. However, Node.js servers have to also deal with TCP streams and reading and writing to the filesystem, both of which make it necessary to deal with purely binary streams of data.

原本JavaScript就傾向於用unicode-encode 編碼來處理字串，甚至於用該編碼來處理TCP/IP 封包內容以及檔案內容的處理