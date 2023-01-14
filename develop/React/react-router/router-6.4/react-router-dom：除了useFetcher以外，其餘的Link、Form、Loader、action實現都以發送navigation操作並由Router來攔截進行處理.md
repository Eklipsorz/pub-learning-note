## 描述


[[@UseFetcherV6]]
> In HTML/HTTP, data mutations and loads are modeled with navigation: \<a href\> and \<form action\>. Both cause a navigation in the browser. The React Router equivalents are \<Link\> and \<Form\>.

> But sometimes you want to call a loader outside of navigation, or call an action (and get the data on the page to revalidate) without changing the URL. Or you need to have multiple mutations in-flight at the same time.

> Many interactions with the server aren't navigation events. This hook lets you plug your UI into your actions and loaders without navigating.

在HTML/HTTP中，資料處理和載入都會由navigation來進行，比如href或者form的action，這些都會導致瀏覽器發生navigation，而在Router則是使用Link和Form元件來發送navigation操作並由Router來攔截。

重點：
- 除了useFetcher以外，其餘的Link、Form、Loader、action實現都以發送navigation操作並由Router來攔截進行處理

## 複習
#🧠 react-router-dom-6.4：除了useFetcher以外，其餘的Link、Form、Loader、action實現都以什麼形式發送？ ->->-> `除了useFetcher以外，其餘的Link、Form、Loader、action實現都以發送navigation操作並由Router來攔截進行處理`
<!--SR:!2023-02-19,36,230-->

---
Status: 
Tags:
Links:
References:
[[@UseFetcherV6]]