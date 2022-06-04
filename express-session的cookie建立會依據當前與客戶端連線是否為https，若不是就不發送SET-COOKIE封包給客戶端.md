

若將cookie內的secure設定為false或者不設定，就會允許伺服器在與使用http協定的客戶端的情況下，發送SET-COOKIE給客戶端
```
app.use(

session({
	store: new RedisStore({ client: redisClient }),
	saveUninitialized: false,
	secret: process.env.SESSION_SECRET,
	resave: false,
	cookie: {
		// secure: true,
		httpOnly: true
	}
})
)
```

 客戶端接收到的回應封包內容：
 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654314707/blog/network/cookie/true-secure-cookie-status_mezro3.png)
 
 反之，若設定secure的話，就只允許伺服器與使用https協定的客戶端，發送SET-COOKIE給客戶端，若只是使用http協定的客戶端與伺服器互動的話，伺服器就不會發送SET-COOKIE給客戶端


 客戶端接收到的回應封包內容：
 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1654314706/blog/network/cookie/false-secure-cookie-status_tu5bfz.png)
 
 
---
Status: #📥 
Tags:
[[Session]] - [[Cookie]] - [[Express]]
Links:
References: