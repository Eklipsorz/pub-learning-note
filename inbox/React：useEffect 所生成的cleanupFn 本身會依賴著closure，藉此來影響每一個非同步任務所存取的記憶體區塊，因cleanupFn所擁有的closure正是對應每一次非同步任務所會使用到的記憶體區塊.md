## 描述


### useEffect 所生成的cleanupFn 本身會依賴著closure


useEffect 所生成的cleanupFn 本身會依賴著closure，藉此來影響每一個非同步任務所存取的記憶體區塊，因cleanupFn所擁有的closure正是對應每一次非同步任務所會使用到的記憶體區塊
```
useEffect(() => {
	let variable;
	// generate a async task
	return cleanupFn
}, [deps])
```



#### 範例

在這裡，每個cleanupFn的產生會因為closure而對應到subscribed這記憶體區塊，而非同步任務也是依據同個記憶體區塊內容來決定是否移動。

```
useEffect(() => {
      let subscribed = true
      something(…)
      .then((….) => {
           if (subscribed) 
           /* do side effect */
       })

      return () => {
          subscribed = false
      } 
}, [deps])
```

## 複習

#🧠 react：useEffect 的cleanup要如何影響每一次非同步任務的執行？ ->->-> `生成一個擁有可儲存當時能夠對應到記憶體區塊的closure之函式物件`
<!--SR:!2022-11-10,3,250-->

---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
[[React：useEffect cleanup 技術主要是停止當前side effect所產生的非同步任務]]
[[React：當元件上註冊了useEffect並觸發unmount，無論dependency是什麼，都會執行cleanup，而非side effect]]
References: