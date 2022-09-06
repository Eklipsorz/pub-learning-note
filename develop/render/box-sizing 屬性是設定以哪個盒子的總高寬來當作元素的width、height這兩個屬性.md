## 描述


[[@mdnBoxsizingCSSMDN]]
> # box-sizing
> The box-sizing property is used to alter the default CSS box model (en-US) used to calculate width and height of the elements. It is possible to use this property to emulate the behavior of browsers that do not correctly support the CSS box model specification.

> box-sizing 屬性用於更改預設 CSS 盒子模型 (en-US)中所計算的寬度和高度。可以使用此屬性來模擬不正確支持 CSS 盒子模型規範的瀏覽器的行為。


> content-box: 
> 
> 這是根據 CSS 標準的起始值和預設值。 width 與 height 只包括內容本身的寬和高， 不包括邊框（border）、內邊距（padding）、外邊距（margin）。注意：內邊距、邊框和外邊距都在這個盒子的外部。例如，如果 .box {width: 350px}; 而且 {border: 10px solid black;}，那麼在瀏覽器中的渲染該容器的實際寬度將是370px，簡單來說，尺寸計算公式：width = 內容的寬度，height = 內容的高度。寬度和高度都不包含內容的邊框（border）和內邊距（padding）。

> border-box : 
> 
> width 和 height 屬性包括內容（content），內邊距（padding）和邊框（border），但不包括外邊距（margin）。這是當文檔處於 Quirks 模式時 Internet Explorer 所使用的盒模型。注意，內邊距和邊框都將在盒子內 ，例如，.box {width: 350px; border: 10px solid black;}，渲染出的容器寬度會固定在 350px，而內容（content）的寬度就會變成 330px，因為邊框（border）佔了20px。內容框不能為負，並且進位到 0，使得不可能使用 border-box 使元素消失。
> 
> 這裡的維度計算為： width = border + padding + 內容的 width， height = border + padding + 內容的 height。 

重點：
- box-sizing：主要設定以哪個盒子的總高寬來當作元素的width、height這兩個屬性，可以填入的分別為：
	- content-box：以content box的總高寬來當作元素的高寬屬性，不包含padding和border
	- border-box ：以border box的總高寬來當作元素的高寬屬性，包含padding和border：
		- width：border-width\*2 + padding-width\*2 + content box的width
		- height：border-height\*2 + padding-height\*2 + context box的height



### box-sizing：content-box

> If we assume that a box has the following CSS:

```
.box {
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
}
```

> The _actual_ space taken up by the box will be 410px wide (350 + 25 + 25 + 5 + 5) and 210px high (150 + 25 + 25 + 5 + 5).


重點：
- 在這裡設定box-sizing 為content-box
- 其width、height會是設定content box的部分
- 元素實際所佔的大小為(content box + padding box本身大小 + border box本身大小)：
	- 寬：(350px + 25\*2 + 5\*2) = 410 px
	- 高：(150px + 25\*2 + 5\*2) = 210 px
- content box所佔的大小為：
	- 寬：350px
	- 高：150px


### box-sizing：border-box

> If we assume that a box has the following CSS:

```
.box {
  width: 350px;
  height: 150px;
  margin: 10px;
  padding: 25px;
  border: 5px solid black;
  box-sizing: border-box
}
```

重點：
- 在這裡設定box-sizing 為border-box
- 其width、height會是設定border box的總高寬部分
- 元素實際所佔的大小為(content box + padding box本身大小 + border box本身大小)：
	- 寬：350px
	- 高：150px
- content box 所佔的大小為
	- 寬：350px - 25\*2  - 5\*2 = 290px
	- 高：150px - 25\*2  - 5\*2 = 90px

## 複習

#🧠 box-sizing 屬性是什麼？ ->->-> `主要設定以哪個盒子的總高寬來當作元素的width、height這兩個屬性`
<!--SR:!2022-09-09,3,250-->

#🧠 box-sizing 屬性可填入什麼屬性值？->->-> `content-box、border-box`
<!--SR:!2022-09-09,3,250-->

#🧠 box-sizing 屬性是content-box，代表著？->->-> `以content box的總高寬來當作元素的高寬屬性，不包含padding和border`
<!--SR:!2022-09-09,3,250-->

#🧠 box-sizing 屬性是content-box，其高寬會包含著什麼？ ->->-> `content-box 高寬`


#🧠 box-sizing 屬性是border-box，代表著 ->->-> `以border box的總高寬來當作元素的高寬屬性，包含padding和border`
<!--SR:!2022-09-09,3,250-->

#🧠 box-sizing 屬性是border-box，其高寬會包含著什麼？ ->->-> `content-box 高寬、padding box本身高寬、border box本身高寬`


#🧠 假如box-sizing是context box，請問元素實際所佔的大小為何？以及content box大小為何![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662479135/blog/css/box-model/box-sizing-question_riexdo.png) ->->-> `- 元素實際所佔的大小為(content box + padding box本身大小 + border box本身大小)： - 寬：(350px + 25\*2 + 5\*2) = 410 px - 高：(150px + 25\*2 + 5\*2) = 210 px - content box所佔的大小為： - 寬：350px - 高：150px`
<!--SR:!2022-09-09,3,250-->


#🧠 假如box-sizing是border box，請問元素實際所佔的大小為何？以及content box大小為何![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1662479135/blog/css/box-model/box-sizing-question_riexdo.png)->->-> ` 元素實際所佔的大小為(content box + padding box本身大小 + border box本身大小)： - 寬：350px - 高：150px - content box 所佔的大小為 - 寬：350px - 25\*2  - 5\*2 = 290px - 高：150px - 25\*2  - 5\*2 = 90px`
<!--SR:!2022-09-09,3,250-->



---
Status:  #🌱 
Tags:
[[CSS]]
Links:
[[每一個HTML 元素都是由多種盒子相互裝載而成的結構，該結構稱之為Box Model]]
References:
[[@mdnBoxsizingCSSMDN]]