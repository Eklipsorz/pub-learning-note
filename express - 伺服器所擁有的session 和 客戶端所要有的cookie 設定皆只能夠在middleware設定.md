


## 描述

若要根據請求來變動cookie和session的設定，以下為嘗試方法
### 嘗試方法
- 在middleware 直接以ioredis來指定對應session的過期時間，會因為對應在redis的session還沒建立好，而過期時間的設定會是失敗的
[[express - redis發送建立對應session來儲存，一開始不會那麼快建立好]]

-  伺服器所擁有的session 和 客戶端所要有的cookie 設定也不能完全透過express-session套件來定義
[[app.use(session(...)) 在一開始會建立對應middleware，之後請求來的時候就以該middleware來處理]]


[[express - 設定cookie的path指定對應cookie內容只能給定特定伺服器下的path]]


### 解法
直接在對應路徑下的middleware之req物件來設定cookie和session

- 設定每個客戶端之cookie的path為/carts 
```
	req.session.cookie.path = '/carts'
```
設定session過期時間(在所有req.session的任一屬性被寫之前放下這段)
```
	req.app.locals.redisStore.ttl = config.days * 86400
```




```
static async getSession(req, _, next) {

	if (req.session && req.session.cartId) {
		return next()
	}

	// build a new session
	const createdAt = new Date()
	const key = `sess:${req.session.id}`
	const config = {
		key, createdAt, days: 7
	}

	req.app.locals.redisStore.ttl = config.days * 86400

	req.session.expireAtConfig = config
	req.session.cookie.path = '/carts'
	req.session.cartId = uuidv4()
	req.session.firstSyncBit = false

	return next()

}

```


另外redisStore本身就含有ttl變數來指定持續時間，參考[[@holowaychukTjConnectredis2022]]:

```
// redis store的建構式：
constructor(options = {}) {

	super(options)
	if (!options.client) {
		throw new Error("A client must be directly provided to the RedisStore")
	}

	this.prefix = options.prefix == null ? "sess:" : options.prefix
	this.scanCount = Number(options.scanCount) || 100
	this.serializer = options.serializer || JSON
	this.client = options.client
	this.ttl = options.ttl || 86400 // One day in seconds.
	this.disableTTL = options.disableTTL || false
	this.disableTouch = options.disableTouch || false

}
```



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[Express]] - [[Redis]]
Links:
[[express - redis發送建立對應session來儲存，一開始不會那麼快建立好]]
[[express - 設定cookie的path指定對應cookie內容只能給定特定伺服器下的path]]
[[app.use(session(...)) 在一開始會建立對應middleware，之後請求來的時候就以該middleware來處理]]
References:
[[@holowaychukTjConnectredis2022]]