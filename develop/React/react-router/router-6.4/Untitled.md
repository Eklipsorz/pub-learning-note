## 描述

[[@UseFetcherV6]]
> In HTML/HTTP, data mutations and loads are modeled with navigation: \<a href\> and \<form action\>. Both cause a navigation in the browser. The React Router equivalents are \<Link\> and \<Form\>.

> But sometimes you want to call a loader outside of navigation, or call an action (and get the data on the page to revalidate) without changing the URL. Or you need to have multiple mutations in-flight at the same time.

> Many interactions with the server aren't navigation events. This hook lets you plug your UI into your actions and loaders without navigating.



> This is useful when you need to:

> -   fetch data not associated with UI routes (popovers, dynamic forms, etc.)
> -   submit data to actions without navigating (shared components like a newsletter sign ups)
> -   handle multiple concurrent submissions in a list (typical "todo app" list where you can click multiple buttons and all should be pending at the same time)
> -   infinite scroll containers
> -   and more!


useFetcher

1. hook

2. avoiding unwanted page transition

so the core idea is really just that we don't trigger any page transition and the fetcher functionality is therefore ideal for pages where you wanna send requests without switching the page

  

  

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