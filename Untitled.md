## 描述

> 當初學者剛接觸 React 時，常常會想要以 inheritance（繼承）的方式來實作 React component。然而 React 官方建議實作 component 時，只應該使用 composition（組合），而不應該使用 inheritance（繼承）。

重點
- React component 是依據著物件導向來開發，所以開發方式具體有兩種：
	- composition
	- inheritance

### composition
> 何謂 composition（組合）

> Composition 是組合的意思。如果一個 class B 中有使用到另一個 class A 創建出來的 instance 的話，就是使用了組合的概念。這時候可以說使用 class A 組合出了 class B 的一部分。

> 更白話的講，composition 代表著 has a（擁有） 的概念。舉例來說，車子擁有引擎，這就是一個經典的 composition 範例。

> Compoistion 各種程式語言中都十分常用的一個技巧。當我們試圖把一個複雜的 class 分割成許多小的區塊時就會常常會使用到 composition 的概念。

重點：
- composition 原意為組合，是代表著 **類別A 有使用到 類別B的實例** 的概念，那麼類別A所建立的實例將會是與類別B的實例的組合物
- 在物件導向語言到關係中，會是代表著 **類別A 擁有(has a)類別B的實例**，舉例車子會擁有引擎
- 適用場景為 
- 將複雜類別A切割成多個獨立且簡單類別B的實例：類別A擁有多個實例B的實例

### composition 優點


> 相較於繼承，composition 的彈性更大，不會被 "is a" 的概念限制，可以只使用自己需要的功能就好，而不必連不需要的功能都一併繼承。

> 除此之外，React 本身提供了很強的 composition 功能。多個 component 可以很輕易的組合成更複雜的 component。

> 其中一個讓 React 有強大 compoisition 功能的原因就是 props 的自由度很高。JavaScript 的各種 primitive value、object、function 乃至 React element 都可以被作為 props 傳給下層的 component 作為顯示 / 執行 / 使用之用。

> 接著，React composition 強大的功能可以把多個任意的 component 組合成一個更複雜的 component。反過來說，也可以很輕易的把一個過於複雜的 component 拆解成較簡單的小 component。因此，藉由善用 composition ，整個 React 專案可以變得更具彈性。這也是為何 React 官方建議使用 composition 而非 inheritance 的原因。


### inheritance

> 何謂 inheritance（繼承）

> Inheritance 是繼承的意思。如果 class B 是基於 class A 衍伸出來（擁有全部 class A 的特性、功能）的話，就是使用了繼承的概念。這時候可以說 class B 繼承了 class A，而 class A 就會被稱為 base class（基礎類別），class B 會被稱為 derived class（衍伸類別）。

> 更白話的講，inheritance 也代表著 is a（是） 的概念。舉例來說，車子是交通工具，這就是一個經典的 inheritance 範例。

> Compoistion 在物件導向（Object Oriented）的語言中十分常見。Inheritance 能夠很好的描繪真實世界的情境，像是貓是一種動物，手機是一部機器等，都是很好描述現實狀況的方式。

> 除此之外，Inheritance 也可以做到依賴反轉的功能，且可以衍伸出多型等強大的樣式供開發者使用。

重點：
- inheritance 是指繼承的意思，是指 **類別 B會是從類別A繼承過來的特性，其類別B擁有全部類別A的所有特性和功能**
- 在物件導向語言的關係中，會是代表著 **類別A 是(is a) 類別B**，舉例來說，車子是交通工具

### ### Inheritance 的缺點

> 然而，撰寫 Inheritance 的時候常常會遇到幾個問題。

> Class 可以想成是一組功能 / 介面的綜合體。當我們使用繼承時，就代表 derived class 必須要完全繼承 base class 的所有功能。當專案剛起步，繼承會看似是一個好選擇，然而隨著需求的演進，會很難保證之後的 derived class 真的會完全符合 base class 的所有介面。如果這時候發現 base class 不夠基本，不符合新的 derived class 設計的話，則會出現兩個解法：

```
-   修改 base class，其他對應的 derived class 也需要一起修改
-   做出不符合 base class 的 derived class，導致怪異的繼承結構
```

重點：
- 繼承類別B的類別A肯定會是擁有類別B的特性和方法，類別A本身會根據需求而朝著不同方式來演化自己所擁有的特性和方法，但具體能不能實現需求就是侷限於類別B
- 面對這侷限問題，會有兩種解法：
	- 考量到還有其他會繼承類別B的類別們，所以會以 **維持base class和幫助類別A實現目標** 的角度來修改類別B，接著也要修改所有類別
	- 不考量到還有其他會繼承類別B的類別們，所以會以 **直接幫助類別A實現目標** 的角度來修改類別B，接著也要修改所有類別，但類別B很有可能演變成怪異的繼承結構
- 這兩種都會面臨 **當一個類別要修改時，其他類別要跟著修改** 的問題，甚至還有使類別B演變成怪異繼承結構的可能



## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References:
