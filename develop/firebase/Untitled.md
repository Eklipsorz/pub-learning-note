## 描述


### Firebase Auth REST API
1. firebase auth rest api 是一個簡單版的auth 認證後端伺服器，以REST風格來提供對應服務


#### API 案例

註冊API端點：
- API_KEY 為 firebase 專案的API KEY
```
https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=[API_KEY]
```




##### 註冊端點使用案例

```
  const submitHandler = async (event) => {
    event.preventDefault();
    const enteredEmail = emailRef.current.value;
    const enteredPasssword = passwordRef.current.value;
    if (isLogin) {
    } else {
      const res = await fetch(
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=[API_KEY]',
        {
          method: 'post',
          headers: { 'content-type': 'application/json' },
          body: JSON.stringify({
            email: enteredEmail,
            password: enteredPasssword,
            returnSecureToken: true,
          }),
        },
      );

      if (res.ok) {
      } else {
        const data = await res.json();
        console.log(data)
      }
      console.log('successfully registered!!')
    }
  };
```




## 複習


---
Status: #🌱 
Tags:
[[Firebase]] - [[Authentication]]
Links:
References: