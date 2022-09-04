
Shopee 找回密碼是以 **信件即為修改密碼的連結** 為主的機制，而非以 **信件內容為驗證碼** 為主的機制。

其正向流程為：
- 使用者輸入email和手機號碼，如果正確的話，伺服器就會寄信
- 伺服器寄修改密碼的連結至對應email
- 使用者在任意瀏覽器都能點擊連結進入修改密碼的環節
- 使用者輸入想要更改的密碼
- 使用者按下確定

申請畫面：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656255967/belazy-shop/example/forgot-password-example/shopee-forgot-password_auynsw.png)

驗證信內容：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656255967/belazy-shop/example/forgot-password-example/shopee-forgot-password-link_igaqzq.png)

修改密碼連結格式為：
	- xxxx 為對應email的驗證碼
	- email 為使用者想要申請找回密碼的電子郵件
```
host/forgot_password/?code=xxxx&<email>
```


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: