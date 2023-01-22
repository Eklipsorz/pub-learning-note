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
	status: 302,
	headers: {
	    Location: path
	}
})
```
- Response 物件和 redirect 本身是個物件，並不會直接讓使用者導向其頁面
- 當Route元件的action屬性值是專門導向的response時，React-router就會自動將使用者導向至對應頁面。

## 複習

#🧠 react-router-dom v6.4：redirect 會是什麼？  ->->-> `redirect 在react-router-dom v6.4裡是一個封裝後的Response 物件`
<!--SR:!2023-03-04,52,250-->
																													
#🧠 react-router-dom v6.4：redirect 在react-router-dom v6.4裡是一個封裝後的Response 物件，其物件會是什麼？？ ->->-> ``
<!--SR:!2023-02-05,21,210-->

#🧠 react-router-dom v6.4： Response 物件和 redirect 本身會直接讓使用者導向其頁面嗎？為什麼？->->-> `並不會，因為他們本身只是回應封包的物件`
<!--SR:!2023-01-22,27,250-->

#🧠 react-router-dom v6.4： Response 物件和 redirect 本身只是回應封包的物件，那要如何導向？->->-> `只有讓React-router收到專門導向的response，React-router就會自動將使用者導向至對應頁面`
<!--SR:!2023-03-24,64,250-->

#🧠 react-router-dom v6.4： Response 物件和 redirect 本身只是回應封包的物件，那要如何導向？請用語法來表示 ->->-> `<Route path=path1 element=element1 action=xxxx /> 其中xxxx為專門處理資料並建立回應封包的函式物件`
<!--SR:!2023-02-05,14,230-->

#🧠  react-router-dom v6.4：Route元件的action若是專門處理資料並建立回應導向封包的函式物件，具體會在處理過程做些什麼？->->-> `接收回應封包，並根據導向地點來做導向`
<!--SR:!2023-02-01,17,210-->




---
Status: #🌱 
Tags:
[[React]]
Links:
References:
[[@RedirectV6]]
