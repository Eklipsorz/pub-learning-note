

## 描述

### deferred vs. not deferred

[[@DeferredDataV6]]
```
async function loader({ params }) {
	return defer({
	  // not deferred:
	  packageLocation: await packageLocationPromise,
	  // deferred:
	  packageLocation: packageLocationPromise,
	});
}
```

重點：
- deferred 就意味著原本要在render前執行的任務內容推遲至執行render的同時才做，具體是依據event loop的關係，而使promise內的任務執行延後，並將對應Promise物件轉移至後頭負責執行render的程式模組來正式負責該Promise的處理請求、回應處理。
- not deferred 就意味著繼續在render前執行loader任務，具體會是以await、指派語句、await promise後的剩餘代碼之間的關係，而剩餘代碼會是指Route執行render。藉此將指派語句、後頭語句由promise.then所包含，使得只有執行完Promise本身才有辦法繼續完成指派、Route執行render，而這情況剛好是由Route元件先執行Loader，再後執行render

[[當在async 函式內碰到指定await promise指派給特定識別字時，await會以分配記憶體來定義存放resolve的結果值，並賦予其識別字1，再以promise.then來設定resolve的結果值指派給識別字1所對應的內容]]

### 問題描述

[[@DeferredDataV6]]
> Imagine a scenario where one of your routes' loaders needs to retrieve some data that for one reason or another is quite slow. For example, let's say you're showing the user the location of a package that's being delivered to their home:

```
import { json, useLoaderData } from "react-router-dom";
import { getPackageLocation } from "./api/packages";

async function loader({ params }) {
  const packageLocation = await getPackageLocation(
    params.packageId
  );

  return json({ packageLocation });
}

function PackageRoute() {
  const data = useLoaderData();
  const { packageLocation } = data;

  return (
    <main>
      <h1>Let's locate your package</h1>
      <p>
        Your package is at {packageLocation.latitude} lat
        and {packageLocation.longitude} long.
      </p>
    </main>
  );
}
```

> We'll assume that `getPackageLocation` is slow. This will lead to initial page load times and transitions to that route to take as long as the slowest bit of data. There are a few things you can do to optimize this and improve the user experience:

> -   Speed up the slow thing (😅).
> -   Parallelize data loading with `Promise.all` (we have nothing to parallelize in our example, but it might help a bit in other situations).
> -   Add a global transition spinner (helps a bit with UX).
> -   Add a localized skeleton UI (helps a bit with UX).

問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟



### 初始解決方案


[[@DeferredDataV6]]
> If these approaches don't work well, then you may feel forced to move the slow data out of the loader into a component fetch (and show a skeleton fallback UI while loading). In this case you'd render the fallback UI on mount and fire off the fetch for the data. This is actually not so terrible from a DX standpoint thanks to useFetcher. And from a UX standpoint this improves the loading experience for both client-side transitions as well as initial page load. So it does seem to solve the problem.


> But it's still sub optimal in most cases (especially if you're code-splitting route components) for two reasons:
> 1.  Client-side fetching puts your data request on a waterfall: document -> JavaScript -> Lazy Loaded Route -> data fetch
> 2.  Your code can't easily switch between component fetching and route fetching (more on this later).

重點：
- 將執行較慢的Loader部分放入component function做呼叫，並且先渲染component一開始的畫面，渲染完之後再觸發執行Loader的部分，等到請求回應到的時候，在重新渲染

- 但仍然是次優解，有兩個原因：
	1. client-side 的資料索求過程必須得跟著其他任務排著隊輪流執行，流程會是
		- 解析結果網頁並渲染
		- 解析JS模組所在並加載初始畫面
		- 根據使用者切換的URL來執行對應Route所要做的事情，如loader、render；
		- 執行完以上內容完之後在發送資料索求請求
	2. 抽離出來的loader代碼很難從component角度和route角度進行切換

#### Client-side navigation ?  page transition
[[@LearnNextJs]]
> Client-side navigation means that the page transition happens _using JavaScript_, which is faster than the default navigation done by the browser.

重點：
-  page transition 會是指定頁面轉換成另一個頁面的過程
- Client-side navigation 是使用javascript而進行的頁面轉場過程

##### transition 命名緣由
> a change from one form or type to another, or the process by which this happens

transition意指從特定形式轉換成另一種形式的過程


### 最終解決方案

> React Router takes advantage of React 18's Suspense for data fetching using the defer Response utility and <Await /> component / useAsyncValue hook. By using these APIs, you can solve both of these problems:

> - Your data is no longer on a waterfall: document -> JavaScript -> Lazy Loaded Route & data (in parallel) 
> - Your can easily switch between rendering the fallback and waiting for the data

> Let's take a dive into how to accomplish this.
> ### Using defer

> Start by adding \<Await \/\> for your slow data requests where you'd rather render a fallback UI. Let's do that for our example above:

```
import {
  Await,
  defer,
  useLoaderData,
} from "react-router-dom";
import { getPackageLocation } from "./api/packages";

async function loader({ params }) {
  const packageLocationPromise = getPackageLocation(
    params.packageId
  );

  return defer({
    packageLocation: packageLocationPromise,
  });
}

export default function PackageRoute() {
  const data = useLoaderData();

  return (
    <main>
      <h1>Let's locate your package</h1>
      <React.Suspense
        fallback={<p>Loading package location...</p>}
      >
        <Await
          resolve={data.packageLocation}
          errorElement={
            <p>Error loading package location!</p>
          }
        >
          {(packageLocation) => (
            <p>
              Your package is at {packageLocation.latitude}{" "}
              lat and {packageLocation.longitude} long.
            </p>
          )}
        </Await>
      </React.Suspense>
    </main>
  );
}
```


> By using these APIs, you can solve both of these problems:
> 1.  Your data is no longer on a waterfall: document -> JavaScript -> Lazy Loaded Route & data (in parallel)
> 2.  Your can easily switch between rendering the fallback and waiting for the data



> So rather than waiting for the component before we can trigger the fetch request, we start the request for the slow data as soon as the user starts the transition to the new route. This can significantly speed up the user experience for slower networks.

發送資料索求請求前不會等待著元件做完渲染，而是只要使用者開始導向至新的Route時，其Route就會開始發送資料索求請求，這加快原本索求資料的速度


> Additionally, the API that React Router exposes for this is extremely ergonomic. You can literally switch between whether something is going to be deferred or not based on whether you include the `await` keyword:

```
return defer({
  // not deferred:
  packageLocation: await packageLocationPromise,
  // deferred:
  packageLocation: packageLocationPromise,
});
```


重點：
- 具體方式為
	- 使用defer 來指定哪些本該要在loader的非同步任務是要推遲在render元件時執行
	- 使用Await元件來包覆著被推遲的非同步任務
	- Suspense元件包覆著Await元件，而Await元件則是定義著被推遲的任務內容如何執行、如何把請求回應轉送至目前所在、將回應結果渲染
- 改善結果：
	1. 資料索求請求並不會完全跟著其他任務排著隊輪流執行，流程變成：
		- 解析結果網頁並渲染
		- 解析JS模組所在並加載初始畫面
		- 根據使用者切換的URL來執行對應Route所要做的事情，如loader、render；在執行對應Route所要做的事情render時，就會發送資料索求請求
	2. 抽離出來的代碼很容易從component和route進行切換：透過defer方法和await是否添加來決定是否其promise要在執行route時執行，還是在component執行：
		- 使用await promiseA會被直接套用在對應loader，並且由於await的關係會把後續的元件渲染被包含在promiseA 的then chain裡頭，必須等到promiseA執行完畢才能執行元件渲染
		- 沒使用await的promise會直接推遲至component內執行，即使放到loader時，也會因為非同步任務的關係，而先執行元件渲染。
```
return defer({
  // not deferred:
  packageLocation: await packageLocationPromise,
  // deferred:
  packageLocation: packageLocationPromise,
});
```



## 複習

#🧠 react-router-dom：route 所執行的loader分成deferred 和 not deferred ，請問各為什麼意思？->->-> `deferred 就意味著原本要在render前執行的任務內容推遲至執行render的同時才做、not deferred 就意味著繼續在render前執行loader任務`
<!--SR:!2023-06-05,104,249-->

#🧠 react-router-dom：route 所執行的loader分成deferred 和 not deferred，deferred 就意味著原本要在render前執行的任務內容推遲至執行render的同時才做，具體會是如何實現？ ->->-> `是依據event loop的關係，而使promise內的任務執行延後，並將對應Promise物件轉移至後頭負責執行render的程式模組來正式負責該Promise的處理請求、回應處理。`
<!--SR:!2023-04-11,33,189-->

#🧠 react-router-dom：route 所執行的loader分成deferred 和 not deferred，deferred 就意味著原本要在render前執行的任務內容推遲至執行render的同時才做，具體會是將對應Promise物件轉移至後頭負責執行render的程式模組來正式負責該Promise的處理請求、回應處理，為何可以轉移Promise？難道不擔心中途執行嗎？ ->->-> `由於event loop的關係，而使promise內的任務執行延後`
<!--SR:!2023-04-02,64,250-->

#🧠 react-router-dom：route 所執行的loader分成deferred 和 not deferred，not deferred 就意味著繼續在render前執行loader任務，具體會是什麼？ ->->-> `會是以await、指派語句、await promise後的剩餘代碼之間的關係，而剩餘代碼會是指Route執行render。藉此將指派語句、後頭語句由promise.then所包含，使得只有執行完Promise本身才有辦法繼續完成指派、Route執行render，而這情況剛好是由Route元件先執行Loader，再後執行render`
<!--SR:!2023-05-11,87,249-->

#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，初步解決方案為何？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png) ->->-> ` 將執行較慢的Loader部分放入component function做呼叫，並且先渲染component一開始的畫面，渲染完之後再觸發執行Loader的部分，等到請求回應到的時候，在重新渲染
<!--SR:!2023-04-08,69,250-->
`

#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，初步解決方案為先渲染後發送請求，但仍是次優解，具體有哪些原因？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png)->->-> ` client-side 的資料索求過程必須得跟著其他任務排著隊輪流執行、抽離出來的loader代碼很難從component角度和route角度進行切換`
<!--SR:!2023-04-14,74,250-->

#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，初步解決方案為先渲染後發送請求，具體流程會是什麼？ ->->-> `	- 解析結果網頁並渲染 - 解析JS模組所在並加載初始畫面 - 根據使用者切換的URL來執行對應Route所要做的事情，如loader、render； - 執行完以上內容完之後在發送資料索求請求`
<!--SR:!2023-04-08,70,250-->

#🧠 transition 命名緣由為何？ ->->-> `transition意指從特定形式轉換成另一種形式的過程`
<!--SR:!2023-05-26,94,230-->

#🧠 page transition 會在網頁會是指什麼？->->-> ` page transition 會是指定頁面轉換成另一個頁面的過程`
<!--SR:!2023-04-14,74,250-->

#🧠 Client-side navigation 在網頁會是什麼？ ->->-> `使用javascript而進行的頁面轉場過程`
<!--SR:!2023-04-24,41,210-->

#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，初步解決方案為先渲染後發送請求，但仍是次優解，還有什麼解法？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png) ->->-> `	- 使用defer 來指定哪些本該要在loader的非同步任務是要推遲在render元件時執行 - 使用Await元件來包覆著被推遲的非同步任務 - Suspense元件包覆著Await元件，而Await元件則是定義著被推遲的任務內容如何執行、如何把請求回應轉送至目前所在、將回應結果渲染`
<!--SR:!2023-03-25,60,250-->

#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，解決方案是採用defer、await、suspense 元件，那麼對於先渲染後發送有什麼改善點？？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png) ->->-> ` 資料索求請求並不會完全跟著其他任務排著隊輪流執行、抽離出來的代碼很容易從component和route進行切換`
<!--SR:!2023-07-16,126,250-->



#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，解決方案是採用defer、await、suspense 元件，擁有資料索求請求並不會完全跟著其他任務排著隊輪流執行這優點，其執行流程會是？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png) ->->-> `- 解析結果網頁並渲染 - 解析JS模組所在並加載初始畫面 - 根據使用者切換的URL來執行對應Route所要做的事情，如loader、render；在執行對應Route所要做的事情render時，就會發送資料索求請求`
<!--SR:!2023-04-23,33,230-->


#🧠 問題描述為當要讓Router 執行對應Route的 特定元件PackageRoute渲染前會有個名為`getPackageLocation`的任務內容要執行，但該任務執行起來會較慢，可能會延遲該特定元件PackageRoute的渲染任務，這致使讓使用者的使用體驗很糟，解決方案是採用defer、await、suspense 元件，擁有抽離出來的代碼很容易從component和route進行切換點，其原理會是？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1671469407/blog/react/react-router/v6/loader/loader-refactor-example1_jwnc9x.png) ->->-> `透過defer方法和await是否添加來決定是否其promise要在執行route時執行，還是在component執行：`
<!--SR:!2023-03-27,41,230-->




---
Status: #🌱 
Tags:
[[React]]
Links:
[[當在async 函式內碰到指定await promise指派給特定識別字時，await會以分配記憶體來定義存放resolve的結果值，並賦予其識別字1，再以promise.then來設定resolve的結果值指派給識別字1所對應的記憶體內容]]
References:
[[@DeferredDataV6]]
[[@LearnNextJs]]