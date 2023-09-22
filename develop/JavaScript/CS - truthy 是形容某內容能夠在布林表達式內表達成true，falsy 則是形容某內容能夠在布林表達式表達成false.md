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
- truthy 是形容詞，是程式開發領域所定義的
- 主要形容能夠在布林表達式內被當作是true的，形容目標為內容，通常會是truthy value來形容能夠在布林表達式內被當作true的值
- 至於哪些內容或者值能夠被當作true，則是由程式語言來制定，以JS來說會是以下面形式來當作true：
	- true
	- 物件參照(位置)/物件本身不為null的物件：如{}、[]
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

重點：
- falsy 是形容詞，主要是程式開發領域上所定義的
- 主要形容能夠在布林表達式內表達false的，形容目標為內容，通常會是以falsy value來形容能夠在布林表達式內被當作false的值
- 至於哪些內容或者值能夠被當作false，則是由程式語言來制定，以JS來說會是以下面形式來當作false：
	- false
	- 物件參照(位置)內容或者物件本身為null的物件：null
	- 數字內容為0的數字：0
	- 字串內容為空字串的字串：""、\`\`、''
	- undefined、NaN也即為被當作false

### 通常什麼時候會以布林表達式來看待？
[[@mdnFalsyMDNWeb]] 所描述：
> JavaScript uses type conversion to coerce any value to a Boolean in contexts that require it, such as conditionals and loops.

重點：
- 由開發者自行指定強制轉換：Boolean(value)
- 特定語法如條件式、loop的條件

## 複習
#🧠 Computer science： truthy 是指什麼？ ->->-> `- truthy 是形容詞，是程式開發領域所定義的 - 主要形容能夠在布林表達式內被當作是true的，形容目標為內容，通常會是truthy value來形容能夠在布林表達式內被當作true的值`
<!--SR:!2024-02-14,363,250-->

#🧠 Computer science： 誰制定哪些value 為 truthy value或者 falsy value ->->-> `程式語言`
<!--SR:!2024-02-07,359,250-->


#🧠 哪些內容會在JS中被當作truthy value (提示：數字、字串、布林值、物件)->->-> `至於哪些內容或者值能夠被當作true，則是由程式語言來制定，以JS來說會是以下面形式來當作true：- true - 物件參照(位置)不為null的物件：如{}、[] - 數字為非0的數字：1、2、3 - 字串內容非空字串的字串："0"、"2"`
<!--SR:!2024-01-17,346,250-->


#🧠  哪些內容會在JS中被當作falsy value (提示：數字、字串、布林值、物件)->->-> `	- false - 物件參照(位置)內容為null的物件：null- 數字內容為0的數字：0- 字串內容為空字串的字串：雙引號、單引號、反引號 - undefined、NaN也即為被當作false`
<!--SR:!2023-11-20,95,210-->


#🧠 JS：請問0是算falsy value？還是truthy value？ ->->-> `算falsy value`
<!--SR:!2025-03-23,548,246-->


#🧠 JS：請問undefined、NaN是算falsy value？還是truthy value？->->-> `是算falsy value`
<!--SR:!2023-10-30,236,246-->


#🧠 字串要怎麼才能夠在JS被當作是falsy value? ->->-> `""、``、''`
<!--SR:!2024-01-09,112,210-->

#🧠 "0" 在JS裏是算falsy value嗎？為什麼？->->-> `會被當作是truthy，若要判定字串為falsy value，字串內容必須為空，但內容是存放0，因此為truthy value`
<!--SR:!2023-10-21,292,250-->

#🧠 空陣列[]、空物件{}算是falsy value嗎？為什麼？ ->->-> `會被當作是truthy，這些都屬於物件和物件參件部分，若物件參照要被當作falsy value，則必須為null，但它們都是指向於一個陣列或者一個物件這物件的位置，並非null，只是陣列內容為空或者物件內容為空`
<!--SR:!2025-03-09,593,250-->


#🧠 JS：通常什麼時候會以布林表達式來看待？->->-> `開發者使用強制轉換或者條件式為主的語法`
<!--SR:!2024-05-21,301,190-->


---
Status: #🌱 
Tags: 
[[JavaScript]]
Links:
References:
[[@mdnTruthyMDNWeb]]
[[@mdnFalsyMDNWeb]]