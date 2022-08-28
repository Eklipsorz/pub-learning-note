## 描述

元件設定style的方法，主要有兩種不同的設定方法：
1.  原生HTML DOM 設定方式
2.  React體系所提供的設定方式：
	-  dynamic inline style


### 原生HTML DOM 設定方式

[[@w3schoolHTMLStyleAttribute]]
> The `style` attribute specifies an inline style for an element.
> 
> The `style` attribute will override any style set globally, e.g. styles specified in the `<style>` tag or in an external style sheet.

`<h1 style="color:blue;text-align:center">This is a header</h1>`

重點：
- 每個元件對應的標籤所擁有style屬性(attribute)，style屬性值(attribute)會是樣式屬性名稱和樣式屬性值所構成的
	- tag1 所擁有的style屬性
	```
	<tag1 style="<css>">content</tag1>
	```
	- style能夠填寫的屬性值形式會是如下，且是用字串來表示，主要用途是以目前指定的樣式屬性來增加以及覆蓋對目前tag1所擁有的樣式屬性：
		- 若是目前指定的樣式屬性是tag1原本所沒有的，就直接增加目前屬性至tag1上
		- 若是目前指定的樣式屬性是tag1原本所有的，就直接以目前屬性值覆蓋至tag1的相同屬性
	```
	property1:value1;property2:value2
	```

###  React體系所提供的設定方式 - dynamic inline style

[[@heidi-liuWeek21React]]
> 直接在 HTML 標籤內加入 style 屬性，例如 `style={}`，但需注意下列幾點：
> -   inline style 裡面放的是 object
> -   只能傳入該元素支援的 inline style
> -   而不能傳入偽元素或 hover
> -   因為是 JavaScript 程式碼，需改為駝峰式命名

```
function Title({ size }) {
  if (size === 'XL') {
    return <h1>hello!</h1>
  }
  return(
    // 兩個大括號包住: JavaScript 程式碼 + 以物件形式
    <h2 style={{
      color: 'blue',
      // 需改為駝峰式命名
      textAlign: 'center'
    }}>hello!</h2>
  )
}
```


style屬性值語法形式：
`<Component style={object} />`

object 會以{}來表示，其屬性名稱和屬性值會搭配css樣式下的屬性名稱和屬性值，設定方式有兩種：

- 使用字串來表示
```
<Component style={{'background-color': 'red'}} />
```
- 使用JS表示屬性的方式，但要使用lower camel case
```
<Component style={{backgroundColor: 'red'}} />
```

重點：
- React 體系上的dynamic inline style 是指在JSX形式，每個元件擁有著可以根據執行情況而變動的style屬性(attribute)，形式會是如下，其中style的屬性值(attribute)是用物件來表示
```
<Component style={object} />
```
- object 內的屬性(property)名稱和屬性(property)值會是指定對應元件下所擁有的樣式屬性名稱(property)和樣式屬性值(property)，其中object 屬性可以用：
	- 字串表示特定樣式屬性名稱、樣式屬性值，比如
	```
	<Component style={{'background-color': 'red'}} />
	```
	- 使用JS表示屬性的方式，但要使用lower camel case
	```
	<Component style={{backgroundColor: 'red'}} />
	```
- React 的 dynamic inline style 主要用途是以目前所指定的樣式屬性值來增加和覆蓋對應元件上的樣式屬性
### 原生HTML DOM 設定方式 vs.  React 體系下的 dynamic inline style
相同點：
- 這兩者都是以目前所指定的樣式屬性值來增加和覆蓋對應元件上的樣式屬性
不同點：
- 原生HTML DOM 設定方式 是用字串表示，React 體系下的 dynamic inline style則是可以混雜字串和JS表示屬性的方法。

## 複習


---
Status: #🌱  
Tags:
[[React]] - [[JavaScript]] - [[CSS]]
Links:
References:
[[@w3schoolHTMLStyleAttribute]]
[[@heidi-liuWeek21React]]