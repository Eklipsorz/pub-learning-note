


## 描述

- 在middleware 直接以ioredis來指定對應session的過期時間，會因為對應在redis的session還沒建立好，而過期時間的設定會是失敗的
[[express - redis發送建立對應session來儲存，一開始不會那麼快建立好]]



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


## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags:
Links:
[[express - redis發送建立對應session來儲存，一開始不會那麼快建立好]]
References: