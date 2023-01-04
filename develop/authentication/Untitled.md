## 描述

how to store token in React?

1. 由於牽涉到許多頁面元件和其他元件的存取，所以得以app-wide形式的狀態來給予各個元件來存取

  

以app-wide形式的狀態，在實作上會考量到涉及的頁面元件和元件數量較多，會使用集中儲存狀態和資訊的元件來共享token給各個元件，如

1. 使用context

2. 使用Redux

  

BTW, the authentication state is also not a state that will change very frequently

認證狀態本身 並不會頻繁地更新，所以很適合使用在不利於頻繁更新場景的Context API


###

context 會有的狀態：

1. token

2. isLoggedIn ：布林值，若true表示目前網站處于登入的狀態；若false表示處於未登入的狀態

方向1：若擁有任意token，就為true；若沒有任意token，就為false

在這裡的任意token都為合法，因為取得任意token的唯一條件就是透過伺服器驗證成功並獲取到的token。

> for that we could simply check if we have a token or not.

> which is true or false telling us whether the current user of this website is logged in or not, and out of the box, the user is not logged in.

3. 用來更改狀態的函式，如更改登入狀態的函式，login/logout

function that allow us to change that state

1.  login: (token) => { }


### 

logout 函式：

設定token為null

```
1.  const logoutHandler = () => {
2.      setToken(null);
3.  }
```


  

login 函式：

設定token為任意token

```
1.  const loginHandler = (token) => {
2.     setToken(token);
3.  }
```


###
```
```
1. 從server獲取permission/access，會將permission/access以React系統來儲存
2. 利用React系統所儲存的permission/access來刷新目前介面，如navigation、header



## 複習


---
Status: #🌱 
Tags:
[[React]] - [[Authentication]]
Links:
References: