修正前代碼：理論上有錯誤會直接執行到res.status(errorCode).json就停止，然後由於那段程式碼被執行完之後並非會被停止，而是繼續以目前錯誤訊息來執行next(error)


```
function APIErrorHandler(error, _, res, next) {
	const errorCode = error.code || DEFAULT_CODE
	const message = error.message || DEFAULT_MESSAGE
	const status = DEFAULT_STATUS
	const data = error.data || DEFAULT_DATA

	console.log(error, status, message, data)
	switch (errorCode) {
		case code.BADREQUEST:
		case code.UNAUTHORIZED:
		case code.FORBIDDEN:
		case code.NOTFOUND:
		case code.SERVERERROR:
		 res.status(errorCode).json({ status, message, data })
		 break
	}
	return next(error)
}
```


修正代碼：為了能夠在執行到res.status(errorCode).json就停止，所以在那段添加了return讓程式碼被執行到完畢後就停止。
```
function APIErrorHandler(error, _, res, next) {
	const errorCode = error.code || DEFAULT_CODE
	const message = error.message || DEFAULT_MESSAGE
	const status = DEFAULT_STATUS
	const data = error.data || DEFAULT_DATA

	console.log(error, status, message, data)
	switch (errorCode) {
		case code.BADREQUEST:
		case code.UNAUTHORIZED:
		case code.FORBIDDEN:
		case code.NOTFOUND:
		case code.SERVERERROR:
		return res.status(errorCode).json({ status, message, data })
	}
	return next(error)
}
```