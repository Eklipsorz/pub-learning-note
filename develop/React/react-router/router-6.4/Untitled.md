## 描述
[[@RedirectV6]]

> ### redirect
 > Because you can return or throw responses in loaders and actions, you can use redirect to redirect to another route.


```
import { redirect } from "react-router-dom";

const loader = async () => {
  const user = await getUser();
  if (!user) {
    return redirect("/login");
  }
};
// It's really just a shortcut for this:

new Response("", {
  status: 302,
  headers: {
    Location: someUrl,
  },
});
```

> It's recommended to use redirect in loaders and actions rather than useNavigate in your components when the redirect is in response to data.


重點：
- redirect 在react-router-dom v6.4裡是一個封裝後的Response 物件，其物件為如下：
	- Response 物件是基於Fetch API而產生的
	- 其內部設定基本的狀態碼、導向位置
```
new Response(body, {
	statuse: 302,
	headers: {
	    Location: path
	}
})
```



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@RedirectV6]]
