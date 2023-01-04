## 描述

### how to store token in React?

1. 由於通過登入驗證後的token會牽涉到許多頁面元件和其他元件的存取，所以得以app-wide形式的狀態來給予各個元件來存取


#### 具體實現
以app-wide形式的狀態，在實作上會考量到涉及的頁面元件和元件數量較多，若貿然使用prop drilling可能使缺失因爲規模關係而放大，會使用集中儲存狀態和資訊的元件來共享token給各個元件，如
1. 使用context
2. 使用Redux

另外認證狀態(含token) 本身並不會頻繁地更新，所以很適合使用在不利於頻繁更新場景的Context API


### 定義認證狀態的context object

context 會有的狀態：
1. token：
	- 型別：字串
	- 用途：從伺服器的登入驗證獲取出來的token
	- 初始值：空字串
2. isLoggedIn ：
	- 型別：布林值
	- 用途：若擁有任意token，就為true；若沒有任意token，就為false。主要讓元件從這狀態切換登入時或者未登入時的內容。
	- 初始值：false
4. 用來更改狀態的函式，如更改登入狀態的函式，login/logout

```
import React from 'react';

const AuthContext = React.createContext({
  token: '',
  isLoggedIn: false,
  login: (token) => {},
  logout: () => {},
});

export default AuthContext;
```


#### isLoggedIn 的判定邏輯

isLoggedIn ：若擁有任意token，就為true；若沒有任意token，就為false

原因為：
1. 在這裡的任意token都為合法，因為取得任意token的唯一條件就是透過伺服器驗證成功並獲取到的token，所以只要不為null就為合法登入或者true；否則為未登入狀態或者false


#### 具體實現

1. 註冊token、isLoggedIn狀態
```
const [token, setToken] = useState(null)
const [isLoggedIn, setIsLoggedIn] = useState(false)
```

2. 定義login 函式：設定token為任意token
```
1.  const loginHandler = (token) => {
2.     setToken(token);
3.  }
```

3. 定義logout 函式：設定token為null
```
1.  const logoutHandler = () => {
2.      setToken(null);
3.  }
```


### 總結

1. 從server獲取permission/access，會將permission/access以React系統來儲存
2. 利用React系統所儲存的permission/access來刷新目前介面，如navigation、header



## 複習

#🧠 在client-server間的authentication過程中獲取到token，客戶端的React該如何儲存？先說概念 ->->-> `會以app-wide形式的狀態來儲存token和其登入狀態`

#🧠 在client-server間的authentication過程中獲取到token，客戶端的React該如何儲存token，概念上會是會以app-wide形式的狀態來儲存token和其登入狀態，具體會是用什麼？ ->->-> `會使用集中儲存狀態和資訊的元件來共享token給各個元件，如 1. 使用context 2. 使用Redux`

#🧠  在client-server間的authentication過程中獲取到token，客戶端的React該如何儲存token，其中為何會使用集中儲存狀態和資訊的元件來共享token給各個元件？ ->->-> `以app-wide形式的狀態，在實作上會考量到涉及的頁面元件和元件數量較多，若貿然使用prop drilling可能使缺失因爲規模關係而放大`

#🧠 在client-server間的authentication過程中獲取到token，客戶端的React該如何儲存token，其中token適合儲存在React的Context API構建的儲存空間嗎？ 為何？->->-> `適合，由於認證狀態(含token) 本身並不會頻繁地更新，所以很適合使用在不利於頻繁更新場景的Context API`


#🧠 在client-server間的authentication過程中獲取到token，若定義context object的話，會有什麼樣的狀態和狀態更新函式？ ->->-> `token、isLoggedIn、更新狀態函式有login、logout`

#🧠 在client-server間的authentication過程中獲取到token，若定義context object的話，會有什麼樣的狀態和狀態更新函式？ 以程式碼來表示->->-> `token、isLoggedIn、更新狀態函式有login、logout`


---
Status: #🌱 
Tags:
[[React]] - [[Authentication]]
Links:
References: