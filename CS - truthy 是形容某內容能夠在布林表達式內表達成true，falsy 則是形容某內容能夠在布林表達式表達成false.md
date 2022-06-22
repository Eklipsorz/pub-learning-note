## 描述



### truthy

[[@mdnTruthyMDNWeb]] 所描述：
> In JavaScript, a truthy value is a value that is considered true when encountered in a Boolean context. All values are truthy unless they are defined as falsy. That is, all values are _truthy_ except false, 0, -0, 0n, "", null, undefined, and NaN.

```
if (true)
if ({})
if ([])
if (42)
if ("0")
if ("false")
if (new Date())
if (-42)
if (12n)
if (3.14)
if (-3.14)
if (Infinity)
if (-Infinity)
```


重點：
- truthy 是形容詞，是程式開發領域所會定義的
- 主要形容能夠在布林表達式內被當作是true的，主要形容目標為內容，通常會是truthy value來形容特定值能在布林表達式內被當作true
- 其truthy value的內容會由程式語言來制定，以JS來說會是以下面形式來當作true
	- true
	- 非null的物件：如{}、[]
	- 數字為非0的數字：1、2、3
	- 字串內容非空字串的字串："0"、"2"


### falsy


[[@mdnFalsyMDNWeb]] 所描述：
> A falsy (sometimes written falsey) value is a value that is considered false when encountered in a Boolean context.

```
if (false)
if (0)
if (-0)
if (0n)
if ("")
if ('')
if (``)
if (null)
if (undefined)
if (NaN)
```



### 通常什麼時候會以布林表達式來看待？
[[@mdnFalsyMDNWeb]] 所描述：
> JavaScript uses type conversion to coerce any value to a Boolean in contexts that require it, such as conditionals and loops.
## 複習
#🧠 Question :: ->->-> ``

---
Status: 
Tags: 
[[JavaScript]]
Links:
References:
[[@mdnTruthyMDNWeb]]
[[@mdnFalsyMDNWeb]]