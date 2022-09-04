Shopee 找回密碼是以 **信件即為修改密碼的連結** 為主的機制，而非以 **信件內容為驗證碼** 為主的機制。


其正向流程為：
- 選擇認證方式為身分證，使用者輸入帳號為身分證，姓名就按當初申請來輸入
- 按下送出並選擇後續驗證碼方式為發送email....
- 伺服器發送email至使用者，使用者收到就會是以更改密碼的連結
- 使用者可以在任何瀏覽器連進該連結來更改密碼
- 點擊進去並輸入密碼
- 確定輸入

申請驗證-1：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656255967/belazy-shop/example/forgot-password-example/momo-forgot-password-step1_dal1pn.png)

申請驗證-2：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656255967/belazy-shop/example/forgot-password-example/momo-forgot-password-step2_xkmnni.png)

收到驗證信內容：
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1656255968/belazy-shop/example/forgot-password-example/momo-forgot-password-link_bfwhnl.png)

驗證信內的連結格式為
 - xxxx (使用secret 來加密使用者資訊而得來的)
```
host/resetByEmailCaptcha.moec?<xxxx>
```


---
Status: #🌱 
Tags:
[[Side Project]]
Links:
References: