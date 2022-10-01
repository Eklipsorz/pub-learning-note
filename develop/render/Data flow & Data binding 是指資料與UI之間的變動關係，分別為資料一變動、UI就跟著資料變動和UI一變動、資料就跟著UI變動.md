## 描述



### 用詞澄清1 - data flow & data binding

[[@youchuanhaoJianDanLiaoYiXiaOnewayData]]
> ### 用詞澄清

> 在開始之前，先針對用詞做兩點澄清。 
>## 澄清一：「data flow」跟「data binding」指的是同一件事。
>
> 換句話說，one-way data flow就是one-way data binding；two-way data binding就是two-way data flow。
>
>這件事其實Facebook的React官方文件就有提到：[[@reactThinkingReactReact]]
>> React’s one-way data flow (also called one-way binding) keeps everything modular and fast.

重點：
- data binding 是指由資料與UI的對應關係，資料決定UI或者UI決定資料
- data flow 是指資料與UI的流動方式，資料一變動，UI就跟著資料一起變動 或者 UI一變動，資料就跟著UI一起變動
- 在這裏data binding 和 data flow 由於都是面向同一件事-資料決定UI 或者UI決定資料，因此會是一樣的說法

### 用詞澄清1 -  data flow & data binding 是指稱某種行為


[[@youchuanhaoJianDanLiaoYiXiaOnewayData]]
> 舉例來說，下面這種句子是不嚴謹、充滿誤會的：
> -   某某框架「是」一個 one-way data binding 框架。 → 不嚴謹的句型，盡量少用。
> 
> 正確的描述方法是這樣：
> -   某某框架讓人「很容易做到」one-way data binding。 → 正確句型。
>
> 溝通上應該避免用「是」句型；用「很容易做到」句型才正確。
> 使用正確的句型有助於理解這兩個詞。這部份後面會再解釋。


重點：
- data flow & data binding 都是指誰決定誰的行為，而非是形容詞
- 正確描述會是
```
某某框架讓人「很容易做到」one-way data binding
```
- 錯誤描述會是
```
某某框架「是」一個 one-way data binding 框架。 → 不嚴謹的句型，盡量少用。
```

### Data Model
1. 當對畫面使用template技術而切分成業務邏輯&資料 和 UI時，此時負責業務邏輯&資料就會是Data Model
2. Data Model 是
	- 定義要與template 網頁結合的資料是什麼類型
	- 定義該資料會擁有什麼樣的功能函式-業務邏輯


### Data binding

[[@youchuanhaoJianDanLiaoYiXiaOnewayData]]
> 有了data model獨立於UI的觀念之後，我們會發現上面兩種作法代表兩種資料的流向（data flow）：
> -   從data model出發，每次更新就同步更新UI（甲方向）
> -   從UI出發，每次更新就同步更新data model（乙方向）
    

> 前端框架與data binding的關係，就是框架本身能否讓人很容易就做出甲方向或是乙方向的效果。
> 
> 能輕易做出其中一個方向，就算是達成one-way data binding。
> 能輕易同時做出兩方向，就算是達成two-way data binding。

[[@mcgarnagleJavascriptWhatTwo]]
> Two-way binding just means that:
>
> 1.  When properties in the model get updated, so does the UI.
> 2.  When UI elements get updated, the changes get propagated back to the model.

![](https://i.stack.imgur.com/2wouW.jpg)

重點：
- data flow & data binding 主要有兩種方向
	- 方向1：資料一改變，UI就跟著資料改變 / 資料決定UI
	- 方向2：UI一改變，資料就跟著UI改變 / UI 決定資料
- 方向2：若狀態、資訊純粹是由UI或者UI互動而產生出來的，那從互動時的該資訊之擷取會是屬於UI一改變，資料就跟著UI改變 / UI 決定資料
- 如果框架只能夠輕易做其中一個方向，就代表該框架容易實現one-way data binding
- 如果框架能輕易做兩個方向，就代表該框架容易實現two-way data binding


### 案例：資料一改變，UI就跟著資料改變 / 資料決定UI

資料model在渲染前被定義好，所以只需要將資料插入至UI，就能產出對應資料的UI，若資料model被改變時，對應的UI也會跟著改變。

```
var PRODUCTS = [
    {category: 'Sporting Goods', price: '$49.99', stocked: true, name: 'Football'},
    {category: 'Sporting Goods', price: '$9.99', stocked: true, name: 'Baseball'},
    {category: 'Sporting Goods', price: '$29.99', stocked: false, name: 'Basketball'},
    {category: 'Electronics', price: '$99.99', stocked: true, name: 'iPod Touch'},
    {category: 'Electronics', price: '$399.99', stocked: false, name: 'iPhone 5'},
    {category: 'Electronics', price: '$199.99', stocked: true, name: 'Nexus 7'}
];

ReactDOM.render(
    <FilterableProductTable products={PRODUCTS} />,
    document.getElementById('container')
);
```



### 案例：UI一改變，資料就跟著UI改變 / UI 決定資料

輸入欄位被人填寫，此時Data Model並沒有該欄位資料，經由輸入欄位的輸入事件後處理來將欄位資料納入資料或者Data Model

```
handleChange: function(event) {
  this.setState({message: event.target.value});
},
```

```
render: function() {
  var message = this.state.message;
  return <input type="text" value={message} onChange={this.handleChange} />;
}
```

## 複習
#🧠 在前端開發中，data binding是什麼意思？ ->->-> `是指由資料與UI的對應關係，資料決定UI或者UI決定資料`
<!--SR:!2022-11-14,52,250-->

#🧠 在前端開發中，data flow是什麼意思？ ->->-> `是指資料與UI的流動方式，資料一變動，UI就跟著資料一起變動 或者 UI一變動，資料就跟著UI一起變動`
<!--SR:!2022-10-02,26,250-->

#🧠 在前端開發中，data binding 和 data flow之間是否一樣？為什麼 ->->-> `是一樣，都同樣面向於資料決定UI或者UI決定資料`
<!--SR:!2022-12-03,63,250-->

#🧠 在前端開發中，data binding 和 data flow 是算形容詞嗎？ ->->-> `並不是，算是某種行為`
<!--SR:!2022-12-05,65,250-->

#🧠 在前端開發中，data binding 和 data flow 是行為，請舉正確案例 ->->-> `某某框架讓人「很容易做到」one-way data binding。`
<!--SR:!2022-10-04,28,250-->

#🧠 某某框架「是」一個 one-way data binding 框架 這說法對於data binding 正確的嗎 ->->-> `不是，因為data binding 本身指的是行為，而不是用來形容用的詞`
<!--SR:!2022-11-22,55,250-->

#🧠 在前端開發中，data model 是什麼？->->-> `當對畫面使用template技術而切分成業務邏輯&資料 和 UI時，此時負責業務邏輯&資料就會是Data Model`
<!--SR:!2022-10-04,28,250-->

#🧠 Data flow：資料一變動，UI就跟著資料一起變動 或者 UI一變動，資料就跟著UI一起變動 這句中的資料在MVC會是什麼？->->-> `Data Model `
<!--SR:!2022-11-24,58,250-->

#🧠 data flow & data binding 主要有兩種方向，是哪兩種？ ->->-> `方向1：資料一改變，UI就跟著資料改變 / 資料決定UI、方向2：UI一改變，資料就跟著UI改變 / UI 決定資料`
<!--SR:!2022-11-28,59,250-->

#🧠 框架容易實現one-way data binding，那麼代表什麼意思？ ->->-> `該框架容易實現- 方向1：資料一改變，UI就跟著資料改變 / 資料決定UI - 方向2：UI一改變，資料就跟著UI改變 / UI 決定資料中的方向之一`
<!--SR:!2022-10-03,27,250-->

#🧠 為何某元件的事件發生時擷取資訊是屬於UI一改變，資料就跟著UI改變 / UI 決定資料？ ->->-> `這是因為該資訊是源自UI本身的互動所產生，並非由資料本身`
<!--SR:!2022-10-07,28,250-->

#🧠 某元件的事件發生時擷取資訊是屬於哪種data binding? ->->-> `UI一改變，資料就跟著UI改變 / UI 決定資料？`
<!--SR:!2022-10-07,28,250-->

#🧠 框架容易實現two-way data binding，那麼代表什麼意思？->->-> `該框架容易實現- 方向1：資料一改變，UI就跟著資料改變 / 資料決定UI - 方向2：UI一改變，資料就跟著UI改變 / UI 決定資料`
<!--SR:!2022-11-25,58,250-->

#🧠 UI一改變，資料就跟著UI改變 / UI 決定資料，請舉出案例來說明？->->-> `綁定於特定元件下來攔截資料，就能以UI一改變就跟著改變資料的案例`
<!--SR:!2022-11-27,59,250-->

#🧠 資料一改變，UI就跟著資料改變 / 資料決定UI，請舉出案例來說明？ ->->-> `藉由定義Data Model以及搭配template，就能得到對應資料的UI，而當Data Model上的資料變動時，就會跟著改變UI`
<!--SR:!2022-12-02,63,250-->


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
References:
[[@reactThinkingReactReact]]
[[@mcgarnagleJavascriptWhatTwo]]
[[@youchuanhaoJianDanLiaoYiXiaOnewayData]]