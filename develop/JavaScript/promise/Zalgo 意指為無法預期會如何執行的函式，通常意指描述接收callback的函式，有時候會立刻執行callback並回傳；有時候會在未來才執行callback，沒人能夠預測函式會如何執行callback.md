## 描述

[[@orenDonReleaseZalgo]]
> Zalgo is a Issac's nickname for a function that is not predictable. What it means is a function that accepts a callback and sometimes returns it right away, and some other times it returns it after some delay, in the future.

解法：
> So when you write a function that accept a callback, make sure your function always sync or always async. don't mix the two.



重點：
- Zalgo 意指為無法預期會如何執行的函式，通常意指描述接收callback的函式，有時候會立刻執行callback並回傳；有時候會在未來才執行callback，沒人能夠預測函式會如何執行callback
- 面對接收callback來執行的函式Zalgo解法可以是：
	- 將callback的執行一律都設定成同步執行或者非同步執行，不能混雜同步執行和非同步執行在執行同一個callback上


#### 範例

若result為以同步執行的話，會印出a=0；若result為以非同步執行的話，會印出a=1。

```
function result(data) {
	console.log(a);
}

var a = 0;

ajax(...., result);
a++;
```


## 複習

#🧠 Zalgo 在程式語言開發上會是指什麼？->->-> `無法預期會如何執行的函式`
<!--SR:!2023-03-07,26,250-->

#🧠 Zalgo 意指為無法預期會如何執行的函式，通常意指為什麼？ 詳細說明->->-> `述接收callback的函式，有時候會立刻執行callback並回傳；有時候會在未來才執行callback，沒人能夠預測函式會如何執行callback`
<!--SR:!2023-03-15,30,250-->

#🧠 面對接收callback來執行的函式Zalgo解法可以是什麼？->->-> `將callback的執行一律都設定成同步執行或者非同步執行`
<!--SR:!2023-02-27,10,250-->

#🧠 面對接收callback來執行的函式Zalgo解法可以是什麼？ 解法上可以混雜同步執行和非同步執行在執行同一個callback上嗎？ 為什麼？ ->->-> `不行，將callback的執行一律都設定成同步執行或者非同步執行`
<!--SR:!2023-02-25,8,250-->



#🧠 請問result各以非同步執行和同步執行，兩者能夠印出的a會是什麼？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674746837/blog/javascript/promise/Zalgo/zalgo-example_vame9u.png) ->->-> `若result為以同步執行的話，會印出a=0；若result為以非同步執行的話，會印出a=1。`
<!--SR:!2023-03-12,29,250-->


#🧠 請問result各以非同步執行和同步執行，兩者能夠印出的a會是什麼？各為1和0，為什麼![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1674746837/blog/javascript/promise/Zalgo/zalgo-example_vame9u.png) ->->-> `主要非同步執行的話，任務排程會被放進queue等待callstack執行完畢才執行，所以會比較晚執行，至少會是在a++做完之後才有辦法輪到它執行；同步執行的話，會直接執行callback，而直接取得a=0來印出。`
<!--SR:!2023-03-08,26,250-->


---
Status: #🌱 
Tags:
[[JavaScript]]
Links:
[[@orenDonReleaseZalgo]]
References: