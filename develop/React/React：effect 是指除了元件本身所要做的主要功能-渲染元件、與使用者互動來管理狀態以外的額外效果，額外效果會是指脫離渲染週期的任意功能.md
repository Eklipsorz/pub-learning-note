## 描述


### React: effect
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]

[[@academindReactcompleteguidecodeButtonModule]]
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663086596/blog/react/effect/react-vs-side-effect_yt8q3n.png)

重點：
- Effect 等同於 Side Effect，effect 本身是指特定處理的結果，在這裡泛指著功能
- Side Effect 是指除了主要效果以外的額外效果：
	- 主要效果會是指元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態，實際上會以元件被執行來產出Virtual DOM至渲染實際DOM結構的循環內所定義的任務內容來當作主要功能
	- 額外效果會是指除了主要效果以外的任意功能，但功能種類會是處於 **脫離元件被執行來產出Virtual DOM至渲染實際DOM結構的循環** 的狀態下才能被正常執行，否則若是在能在那循環內執行的話，就會被React視為主要功能而執行 或者 遇到無限循環的問題
	- Side Effect 案例：
		- 在瀏覽器儲存空間內儲存資料
		- 傳遞請求至後端伺服器，然後接收到回應就觸發狀態更新。



### 潛在問題

#### effect 實現代碼放進渲染週期函式的話
> if we would send a http reqest
> Then we would send this request whenever this function re-runs.

> -> 每當這個函式重複執行，就會發送請求

> So for example, whenever this state changes and might sometimes be what you want but definitely not always. And if in response to your http request

> you for example eventually change some state, you would even create an infinite loop



如果effect 實現代碼會是發送http 請求，並且以回應觸發渲染週期，接著在把其實現代碼放進渲染週期函式的話，會衍生出無限重複呼叫：
	- 一開始執行元件的渲染週期函式來開始渲染，並發送請求，接著渲染當前元件
	- 等到請求回應傳到元件，就觸發渲染週期
	- 由於觸發渲染，又再一次呼叫渲染週期函式，接著又發送請求，渲染當前元件
	- 等到請求回應傳到元件，就觸發渲染週期
	- 後面全都是這兩個

```
render() {

	// send a request

	// handler 
	const requestHandler = () => {
		setXXXX(XXXX);
	}

	// template
	return (
		....
	)
}
```

#### 總結
但如果排除掉http請求和回應的話，只要是能夠觸發渲染週期的side effect 放在渲染週期函式皆會有無限迴圈的問題，然而本身並不會觸發渲染週期的side effect 放在渲染週期函式 本身會因為不會再次呼叫渲染週期函式而不會有無限迴圈的問題。


總結：
- 只要是能夠觸發渲染週期的side effect 放在 渲染週期函式的話，就會有無限迴圈的潛在問題
- 只要不能夠渲染週期的side effect 放在 渲染週期函式的話，就不會有無限迴圈的潛在問題


#### 解法

將能夠觸發渲染週期的side effect 另外設定額外條件來執行(除了進入渲染週期以外的條件)，比如：
- 判定某些指定內容是否有改變，有改變就執行；沒改變就不執行
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]

	~~- function component：使用useEffect所建立的執行環境~~
	~~- class：使用生命週期函式，通常會放在~~
		~~- componentDidMount
		- componentDidUpdate
		- componentWillUnmount~~

整體來說，side effect的執行條件為：
- 進入渲染週期的特定函式
- 判定某些指定內容是否有改變，有改變就執行；沒改變就不執行

#### 現實層面
通常會想透過effect來實現功能的實例會是前端向後端伺服器請求並以其請求回應觸發渲染，而使用頻率極為常見，並且這樣等同於需要能夠觸發渲染週期的side effect ，因此才必須考慮side effect要在哪個條件下執行。

## 複習

#🧠 在React中，side effect 是指什麼？ ->->-> `Side Effect 是指除了主要效果以外的額外效果，主要效果會是指元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態`
<!--SR:!2022-09-28,10,250-->

#🧠 在React中，side effect 是指除了主要效果以外的額外效果，那麼額外效果是指什麼？？ ->->-> `額外效果會是指除了主要效果以外的任意功能`
<!--SR:!2022-10-12,17,250-->

#🧠 在React中，effect 會跟 side effect 一樣嗎？ ->->-> `對`
<!--SR:!2022-09-28,10,250-->

#🧠 在React中，side effect 是指除了主要效果以外的額外效果，那麼主要效果會在什麼時期下執行？？ ->->-> `會以元件被執行來產出Virtual DOM至渲染實際DOM結構的循環內`
<!--SR:!2022-10-23,26,250-->

#🧠 在React中，side effect 是指除了主要效果以外的額外效果，主要效果會是元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態，那麼實際上那要如何被當作主要功能 ->->-> `會以元件被執行來產出Virtual DOM至渲染實際DOM結構的循環內所定義的任務內容來當作主要功能`
<!--SR:!2022-10-23,26,250-->


#🧠 在React中，side effect 是指除了主要效果以外的額外效果，額外效果會處於什麼狀態下執行？ ->->-> `功能種類會是處於**脫離元件被執行來產出Virtual DOM至渲染實際DOM結構的循環** 的狀態`
<!--SR:!2022-10-22,25,250-->

#🧠 在React中，effect實現代碼會放進渲染週期，會容易遇到什麼潛在問題？ ->->-> `若effect本身能夠觸發渲染週期，就會有無限迴圈的潛在問題`
<!--SR:!2022-10-25,27,250-->

#🧠 在React中，effect實現代碼為什麼普遍要脫離渲染週期的狀態，持續待在渲染週期會有什麼潛在問題？ ->->-> `若effect本身能夠觸發渲染週期，就會有無限迴圈的潛在問題`
<!--SR:!2022-10-23,26,250-->

#🧠 在React中，effect本身是會觸發渲染週期的話，並放在渲染週期的相關函式執行，請問如何防止潛在的無限迴圈問題 ->->-> `將能夠觸發渲染週期的side effect 另外設定額外條件來執行(除了進入渲染週期以外的條件)`
<!--SR:!2022-10-25,27,250-->

#🧠 在React中，effect本身是會觸發渲染週期的話，並放在渲染週期的相關函式執行，防止潛在的無限迴圈問題是設定條件來決定執行，那麼整體的條件會是？ ->->-> `- 進入渲染週期的特定函式 - 判定某些指定內容是否有改變，有改變就執行；沒改變就不執行`
<!--SR:!2022-09-28,10,250-->


#🧠 在React中，side effect 的實現代碼若一直處於渲染週期執行的話，會被React視為什麼？ ->->-> `React的主要任務：渲染元件、與使用者互動來管理狀態`
<!--SR:!2022-10-26,28,250-->

#🧠 在React中，Side Effect 常見案例是什麼？->->-> `		- 在瀏覽器儲存空間內儲存資料 - 傳遞請求至後端伺服器，然後接收到回應就觸發狀態更新。`
<!--SR:!2022-10-09,15,230-->


#🧠 React：假如effect 實現代碼會是發送http請求，並且以回應來觸發渲染週期，接著把該實現代碼放進渲染週期的函式，勢必會有無限迴圈的問題，請詳細說明為何有->->-> `	- 一開始執行元件的渲染週期函式來開始渲染，並發送請求，接著渲染當前元件 - 等到請求回應傳到元件，就觸發渲染週期 - 由於觸發渲染，又再一次呼叫渲染週期函式，接著又發送請求，渲染當前元件 - 等到請求回應傳到元件，就觸發渲染週期 - 後面全都是這兩個`
<!--SR:!2022-10-26,28,250-->


#🧠 React：描述一下 side effect 能否觸發和無限迴圈的潛在問題可能之間的關係->->-> `- 只要是能夠觸發渲染週期的side effect 放在 渲染週期函式的話，就會有無限迴圈的潛在問題 - 只要不能夠渲染週期的side effect 放在 渲染週期函式的話，就不會有無限迴圈的潛在問題`
<!--SR:!2022-10-13,18,250-->





---
Status: #🌱 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：useEffect & Dependencies 之間關係就在於每一次在updating階段時effect被觸發時會檢查是否有任一dependency有改變而執行對應的callback]]
[[瀏覽器發送後端請求，回應之前，會先有預設畫面瀏覽給客戶端來增加使用體驗，而非等到回應才渲染，隨後等到回應到來後，就重新渲染]]
References:
[[@academindReactcompleteguidecodeButtonModule]]