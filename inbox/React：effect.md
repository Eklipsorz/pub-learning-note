## 描述


### React: effect
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]



[[@academindReactcompleteguidecodeButtonModule]]
![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663086596/blog/react/effect/react-vs-side-effect_yt8q3n.png)

重點：
- Effect 等同於 Side Effect
- Side Effect 是指除了主要效果以外的額外效果：
	- 主要效果會是指元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態，實際上會以元件被執行來產出Virtual DOM至渲染實際DOM結構的循環內所定義的任務內容來當作主要功能
	- 額外效果會是指除了主要效果以外的任意功能，但功能種類會是處於 **脫離元件被執行來產出Virtual DOM至渲染實際DOM結構的循環** 的狀態下才能被正常執行，否則若是在能在那循環內執行的話，就會被React視為主要功能而執行
	- Side Effect 案例：
		- 在瀏覽器儲存空間內儲存資料
		- 傳遞請求至後端伺服器，然後接收到回應就觸發狀態更新。



### effect 使用方法

#### function component

`useEffect(callback, [dependencies])`

useEffect 語法：

- 第一個引數為callback，這些callback只會在dependencies 改變的時候才執行，而不是在component重新渲染的時候呼叫

> a function that should be executed AFTER every component evaluation IF the specified dependencies changes

-  第二個引數為設定哪些dependencies 改變才會觸發前面的callback，會用陣列來表示所有的dependencies

> dependencies of this effect - the function only runs if the dependencies changed

  





### effect 實現代碼放進render的話
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
但如果排除掉http請求和回應的話，只要是能夠觸發狀態和渲染的side effect 放在render 皆會有無限迴圈的問題。



而這也是為什麼不能把side effect 直接放在component的render，因為會造成額外的無限迴圈。當然若考量到其他更新的方式，只要 請求放在render部分，就還是會衍生出以下循環

呼叫元件的render -> 請求 -> 請求回應 -> 呼叫元件的render -> 請求 -> 請求回應 -> 呼叫元件的render ......

  

如果在沒使用useEffect的情況下，發送http 請求

因為會造成無限迴圈，所以才額外製造一個hook或者特定執行環境

useEffect() is hook：

1. 基於hook而內建

  





## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
References:
[[@academindReactcompleteguidecodeButtonModule]]