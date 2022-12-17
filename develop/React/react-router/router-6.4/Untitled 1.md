
## 描述


> If these approaches don't work well, then you may feel forced to move the slow data out of the loader into a component fetch (and show a skeleton fallback UI while loading). In this case you'd render the fallback UI on mount and fire off the fetch for the data. This is actually not so terrible from a DX standpoint thanks to useFetcher. And from a UX standpoint this improves the loading experience for both client-side transitions as well as initial page load. So it does seem to solve the problem.



將執行較慢的Loader部分放入component function做呼叫，並且先渲染component一開始的畫面，並觸發執行Loader的部分，等到請求到的時候，在重新渲染




> But it's still sub optimal in most cases (especially if you're code-splitting route components) for two reasons:

1.  Client-side fetching puts your data request on a waterfall: document -> JavaScript -> Lazy Loaded Route -> data fetch
2.  Your code can't easily switch between component fetching and route fetching (more on this later).

但仍然是次優解，有兩個原因：
1. client-side 的資料索求過程必須得跟著其他任務排著隊進行，流程會是
1. 你的代碼很難從component和route進行切換


> Client-side navigation means that the page transition happens _using JavaScript_, which is faster than the default navigation done by the browser.

客戶端頁面導向會是使用javascript而進行的頁面轉場過程




### transition 命名緣由
> a change from one form or type to another, or the process by which this happens

transition意指從特定形式轉換成另一種形式的過程


https://reactrouter.com/en/main/guides/deferred

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]]
Links:
References: