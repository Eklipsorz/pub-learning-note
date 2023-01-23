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


### 回應：
idToken 為 JWT 形式的token
```
idToken  string  A Firebase Auth ID token for the authenticated user.
```
## 複習


#💻 請到/githubRepo/react-builder/question-review/react-auth-question 領取題目並切換至build-register-and-login-practice分支，請在/src/components/Auth下的AuthForm增加帳密註冊、登入功能，請調用Firebase上的Authentication REST API來用，功能為：註冊、登入、顯示處理中 ->->-> `https://github.com/academind/react-complete-guide-code/tree/22-authentication/code/04-adding-user-login`
<!--SR:!2023-02-24,32,250-->



---
Status: #🌱 
Tags:
[[React]] - [[Authentication]] - [[Firebase]]
Links:
[[Firebase Auth REST API + REACT 實現註冊頁面]]
References:
