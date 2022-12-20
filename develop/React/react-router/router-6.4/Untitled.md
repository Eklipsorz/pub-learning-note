## 描述

[[@UseFetcherV6]]
> In HTML/HTTP, data mutations and loads are modeled with navigation: \<a href\> and \<form action\>. Both cause a navigation in the browser. The React Router equivalents are \<Link\> and \<Form\>.

> But sometimes you want to call a loader outside of navigation, or call an action (and get the data on the page to revalidate) without changing the URL. Or you need to have multiple mutations in-flight at the same time.

> Many interactions with the server aren't navigation events. This hook lets you plug your UI into your actions and loaders without navigating.

在HTML/HTTP中，資料處理和載入都會由navigation來進行，比如href或者form的action，這些都會導致瀏覽器發生navigation，而在Router則是使用Link和Form元件來發送navigation操作並由Router來攔截。

但有時候你不太想透過navigation或者不太想透過更改URL來呼叫執行loader或者執行action，大部分與伺服器互動都不會是navigation事件，這個hook可以讓你在不用navigation的情況下將你的UI安裝至action和loader

> This is useful when you need to:

> -   fetch data not associated with UI routes (popovers, dynamic forms, etc.)
> -   submit data to actions without navigating (shared components like a newsletter sign ups)
> -   handle multiple concurrent submissions in a list (typical "todo app" list where you can click multiple buttons and all should be pending at the same time)
> -   infinite scroll containers
> -   and more!


> ## `fetcher.submit()`

> The imperative version of `<fetcher.Form>`. If a user interaction should initiate the fetch, you should use `<fetcher.Form>`. But if you, the programmer are initiating the fetch (not in response to a user clicking a button, etc.), then use this function.

> ## [](https://reactrouter.com/en/main/hooks/use-fetcher#fetcherform)`fetcher.Form`

> Just like `<Form>` except it doesn't cause a navigation. (You'll get over the dot in JSX ... we hope!)
```
function SomeComponent() {
  const fetcher = useFetcher();
  return (
    <fetcher.Form method="post" action="/some/route">
      <input type="text" />
    </fetcher.Form>
  );
}
```

重點：
- useFetcher 是 react-router-dom 的hook
- 主要會回傳一個fetcher物件，透過該物件可以不必透過切換URL或者navigation來執行loader或者action
- 主要語法有
	- 若是由使用者互動本身就引發fetch，就使用fetcher.Form
	- 若是想由程式碼引發fetch，就使用fetch.submit，具體是手動


useFetcher

1. hook

2. avoiding unwanted page transition

> so the core idea is really just that we don't trigger any page transition and the fetcher functionality is therefore ideal for pages where you wanna send requests without switching the page

useFetcher 核心概念為在切換頁面的情況下來發送請求並處理

  

> this hook can be used to basically manually trigger a form submission or build a form by using fetcher.Form

you can also use it to manually trigger a loader from inside a component

  

the difference: useFetcher + form   vs. fetcher.Form:

1. when using fetcher for submitting the form instead of using that regular form component

2. will now cause no page transition. but instead, the request is basically sent behind the scenes






## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:

References:
[[@UseFetcherV6]]