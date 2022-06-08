


執行app.js時，會先執行session來建立對應的middleware，接著請求來時就以該middleware來處理，而非以session(sessConfig )
```
app.use(
	session(sessConfig)
)
```

---
Status: #🌱 
Tags:
[[Express]] - [[Session]]
Links:
References: