


## 描述
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]
> ## 多次setState函数调用产生的效果会合并

> 比如下面的代码。

```text
function updateName() {
  this.setState({FirstName: 'Morgan'});
  this.setState({LastName: 'Cheng'});
}
```

> 连续调用了两次this.setState，但是只会引发一次更新生命周期，不是两次，因为React会将多个this.setState产生的修改放在一个队列里，缓一缓，攒在一起，觉得差不多了再引发一次更新过程。


> 在每次更新过程中，会把积攒的setState结果合并，做一个merge的动作，所以上面的代码相当于这样。

```text
function updateName() {
  this.setState({FirstName: 'Morgan', LastName: 'Cheng'});
}
```

> 如果每一个this.setState都引发一个更新过程的话，那就太浪费了！
> 
> 对于开发者而言，也可以放心多次调用this.setState，每一次只要关注当前修改的那一个字段就行，反正其他字段会合并保留，丢不掉。  
> 
> 所以，合并多次this.setState调用更改的状态这个API设计决定也不错。
> 
> **总结一下，setState最招骂的就是不会立即修改this.state。**
> 
> 如果有可能的话，怎么改进这个API呢？
>
>首先setState肯定还是不能立刻更新this.state，不然React整个概念就被推翻了，所以能做的只是用一个更清楚的方式表达，让开发者不会误以为this.state会被this.setState立即更新，好像也没有特别好的改进方法。
>
>不过，最近一个this.setState函数的隐藏功能进入了大家的视野，那就是：**原来this.setState可以接受一个函数作为参数啊！**

重點：
- setState 每一次呼叫時，會生成以下指定任務內容的非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染
	- 更新指定狀態值
- 當沒有再度接收setState時，非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期


### 實際實現 1 - 將狀態更新任務放置佇列

- setState **每一次呼叫時，會生成非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染** 
- 實際實現為：每當執行到setState就先按下面來做
	- 若狀態是以單一值來儲存的話，就直接拿目前任務的狀態去覆蓋先前任務所記錄的狀態
	- 若狀態是以多屬性的物件來儲存的話：
		- 一開始會定義結果物件為空物件
		- 拿目前任務的狀態-物件屬性去追加/覆蓋至結果物件上目前的屬性區分

### 實際實現 2 - 處理佇列的任務

**當非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期** 

- 實際實現為：當目前可以合併的指令都完成合併時，就執行
	- 以目前結果狀態來觸發實際狀態更新 & 渲染。



### 案例 1
假如系統執行以下setState，而狀態會是以物件來表示
```
	function updateName() {
	  this.setState({FirstName: 'Morgan'});
	  this.setState({LastName: 'Cheng'});
	}
```

執行第一個this.setState指令任務，會先將結果物件設定為空物件，並將該任務要求更改的狀態值追加至空物件，做完就做第二個
```
// 追加前
{}
// 追加後
{ FirstName: 'Morgan' }
```

執行第二個this.setState指令任務，會先將任務要求更改的狀態追加/覆蓋至空物件，做完就看有沒有第三個
```
// 追加前 
{ FirstName: 'Morgan' }
// 追加後
{ FirstName: 'Morgan', LastName: 'Cheng' }
```

做完發現沒了，就直接讓負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染

### 案例 2

假如系統執行以下setState，而狀態會是以單一值來表示
```
	function updateName() {
	  // count = 1
	  this.setState(count + 1);
	  this.setState(count + 2);
	  this.setState(count + 3);
	}
```


執行第一個this.setState指令任務，會先將結果物件設定為 1
```
// 追加前
undefined
// 追加後
1
```
執行第二個this.setState指令任務，會先將結果物件設定為 2
```
// 追加前
1
// 追加後
2
```

執行第三個this.setState指令任務，會先將結果物件設定為 3
```
// 追加前
2
// 追加後
3
```

做完發現沒了，就直接負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染

### useState 何時觸發執行？
[[@vencovskyAnswerWhenUse2019]]

> useCallback
> On every render, everything that's inside a functional component will run again.

重點：
- 每一次執行元件的render函式就會執行useState，首次mount階段會以初始值來表示，update階段則是會以新狀態來回傳





## 複習

#🧠 React：setState 每一次呼叫時，概念會如何執行 ->->-> `會生成以下指定任務內容的非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染，指定任務內容為更新指定狀態值，當沒有再度接收setState時，非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期`
<!--SR:!2022-12-12,70,250-->

#🧠 React： setState **每一次呼叫時，會生成非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染** ，若狀態皆為單一值的話，其實際實現為何？->->-> `若狀態是以單一值來儲存的話，就直接拿目前任務的狀態去覆蓋先前任務所記錄的狀態`
<!--SR:!2022-12-16,74,250-->


#🧠 React： setState **每一次呼叫時，會生成非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染** ，若狀態皆為物件的話，其實際實現為何？ ->->-> `一開始會定義結果物件為空物件、拿目前任務的狀態-物件屬性去追加/覆蓋至結果物件上目前的屬性區分`
<!--SR:!2022-12-16,74,250-->

#🧠 React：請問setState 每一次呼叫時會立刻更新state嗎？ 為何？->->-> `並不會，具體要等所有狀態更新指令以batching形式執行完畢後並且觸發updating生命週期函式才會執行更新`
<!--SR:!2022-12-16,74,250-->

#🧠 React： **當非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期** ，其實際實現為何？ ->->-> `實際實現為：當目前可以合併的指令都完成合併時，就執行以目前結果狀態來觸發實際狀態更新 & 渲染。`
<!--SR:!2022-12-15,73,250-->


#🧠 React：負責處理儲存多個狀態更新任務佇列的非同步任務X何時會做狀態更新&渲染 ->->-> `等到沒有狀態更新任務可被執行，就開始執行`
<!--SR:!2022-12-16,74,250-->

#🧠 React18：假如系統執行以下setState，而狀態會是以單一值來表示，那麼過程會是如何執行狀態更新![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-value-example_tw7yp7.png) ->->-> `執行第一個this.setState指令任務，會先將結果物件設定為 2、執行第二個this.setState指令任務，會先將結果物件設定為 ˇ、執行第三個this.setState指令任務，會先將結果物件設定為 4、做完發現沒了，就直接負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染`
<!--SR:!2022-12-12,71,250-->

#🧠 React18：假如系統執行以下setState，而狀態會是以物件來表示，那麼過程會是如何執行狀態更新![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `執行第一個this.setState指令任務，會先將結果物件設定為空物件，並將該任務要求更改的狀態值追加至空物件，做完就做第二個。執行第二個this.setState指令任務，會先將任務要求更改的狀態追加/覆蓋至空物件，做完就看有沒有第三個。做完發現沒了，就直接讓負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染`
<!--SR:!2022-12-13,71,250-->

#🧠 React18：假如系統執行以下setState，而狀態會是以單一值來表示，那麼會以何種狀態來渲染和更新狀態？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-value-example_tw7yp7.png) ->->-> `4`
<!--SR:!2022-12-16,74,250-->

#🧠 React18：假如系統執行以下setState，而狀態會是以物件來表示，那麼會以何種狀態來渲染和更新狀態![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `{ FirstName: 'Morgan', LastName: 'Cheng' }`
<!--SR:!2022-12-13,72,250-->


#🧠 React useState 何時觸發執行？ ->->-> `每一次執行元件的render函式就會執行useState`

#🧠 React useState 每次觸發執行所回傳的狀態會是？ ->->-> `首次mount階段會以初始值來表示，update階段則是會以新狀態來回傳`

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]
References:
[[@gaearonAutomaticBatchingFewer]]
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]