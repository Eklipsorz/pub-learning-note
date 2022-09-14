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

#### effect 實現代碼放進render的話
> if we would send a http reqest
> Then we would send this request whenever this function re-runs.

> -> 每當這個函式重複執行，就會發送請求

> So for example, whenever this state changes and might sometimes be what you want but definitely not always. And if in response to your http request

> you for example eventually change some state, you would even create an infinite loop



如果effect 實現代碼會是發送http 請求，並且以回應作為狀態更新渲染，接著在把其實現代碼放進render的話，會衍生出無限重複呼叫：
	- 一開始執行元件的render來開始渲染，並發送請求，接著渲染當前元件
	- 等到請求回應傳到元件，就觸發狀態更新和渲染
	- 由於觸發渲染，又再一次呼叫render，接著又發送請求，渲染當前元件
	- 等到請求回應傳到元件，就觸發狀態更新和渲染
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
但如果排除掉http請求和回應的話，只要是能夠觸發狀態更新和渲染的side effect 放在render 皆會有無限迴圈的問題，然而本身並不會觸發狀態更新和渲染的side effect 放在render 本身會因為不會再次呼叫render而不會有無限迴圈的問題。


總結：
- 只要是能夠觸發狀態更新和渲染的side effect 放在 render 或者 function component內部的話，就會有無限迴圈的潛在問題
- 只要不能夠觸發狀態更新和渲染的side effect 放在 render 或者 function component內部的話，就不會有無限迴圈的潛在問題


#### 解法

將能夠觸發狀態更新和渲染的side effect 改放進一個獨立的執行環境，比如
	- function component：使用useEffect所建立的執行環境
	- class：使用生命週期函式，通常會放在
		- componentDidMount
		- componentDidUpdate
		- componentWillUnmount

#### 現實層面
通常會想透過effect來實現功能的實例會是前端向後端伺服器請求並以其請求回應觸發渲染，而使用頻率極為常見，並且這樣等同於需要能夠觸發狀態更新和渲染的side effect ，因此才必須考慮side effect要在哪個執行環境執行。

## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References:
[[@academindReactcompleteguidecodeButtonModule]]