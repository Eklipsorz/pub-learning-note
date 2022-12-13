## 描述


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
It's really just a shortcut for this:

new Response("", {
  status: 302,
  headers: {
    Location: someUrl,
  },
});
```

> It's recommended to use redirect in loaders and actions rather than useNavigate in your components when the redirect is in response to data.




## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: