## 描述


### 註冊/登入端點 切換


```
    if (isLogin) {
      url =
        'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=xxx';
    } else {
      url =
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=xxx';
    }
```

### 註冊/登入 fetch重構

```
 const submitHandler = async (event) => {
    event.preventDefault();

    const enteredEmail = emailRef.current.value;
    const enteredPassword = passwordRef.current.value;
    setIsLoading(true);
    let url = '';

	
    if (isLogin) {
      url =
        'https://identitytoolkit.googleapis.com/v1/accounts:signInWithPassword?key=xxx';
    } else {
      url =
        'https://identitytoolkit.googleapis.com/v1/accounts:signUp?key=xxx';
    }

    try {
      const res = await fetch(url, {
        method: 'post',
        headers: { 'content-type': 'application/json' },
        body: JSON.stringify({
          email: enteredEmail,
          password: enteredPassword,
          returnSecureToken: true,
        }),
      });

      const data = await res.json();
      setIsLoading(false);
      if (res.ok) {
        console.log(data);
      } else {
        if (data && data.error && data.error.message)
          throw new Error(data.error.message);
      }
    } catch (error) {
      alert(error.message);
    }
  };
```


## 複習





---
Status: #🌱 
Tags:
[[React]] - [[Authentication]] - [[Firebase]]
Links:
[[Firebase Auth REST API + REACT 實現註冊頁面]]
References:
