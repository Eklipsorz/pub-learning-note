

設定cookie.path為/carts
```
static async getSession(req, _, next) {

	if (req.session && req.session.cartId) {
		console.log('ans:', req.session)
		return next()
	}

	req.session.cartId = uuidv4()
	req.session.firstSyncBit = false
	const createdAt = new Date()
	const key = `sess:${req.session.id}`

	const config = {
		key, createdAt, days: 7
	}

	req.session.expireAtConfig = config
	req.session.cookie.path = '/carts'
	return next()

}

```


若設定cookie.path 為 path的話，在/carts路徑下會獲取下面訊息，其中出現cartId表示客戶端已經儲存對應path路徑的cookie
```
ans: Session {
  cookie: {
    path: '/carts',
    _expires: null,
    originalMaxAge: null,
    httpOnly: true,
    secure: false
  },
  cartId: '9b72a250-d0ea-469a-a3b0-455f4f5906af',
  firstSyncBit: false,
  expireAtConfig: {
    key: 'sess:upTFpMNuRSvMJsS96BPuFjBqegpacTPK',
    createdAt: '2022-06-08T00:58:43.608Z',
    days: 7
  }
}
```


若在別的路徑則是如下，由於路徑並不是/carts，所以接收不到專屬於/carts的cookie內容

```
ans: Session {
  cookie: {
    path: '/',
    _expires: null,
    originalMaxAge: null,
    httpOnly: true,
    secure: false
  }
}
```