



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
- 當非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期


- setState 每一次呼叫時，會生成以下指定任務內容的非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染：
	- 實際實現為：每當執行到setState就先按下面來做
		- 若狀態是以單一值來儲存的話，就直接拿目前任務的狀態去覆蓋先前任務所記錄的狀態
		- 若狀態是以多屬性的物件來儲存的話：
			- 一開始會定義結果物件為空物件
			- 拿目前任務的狀態-物件屬性去追加/覆蓋至結果物件上目前的屬性茲分
	




### 案例2



### 案例 1
假如系統執行以下setState，首先執行第一個就先以建立修改FirstName的非同步任務放進佇列，接著建立完就先執行第二個來建立修改LastName的非同步任務放進佇列
```
	function updateName() {
	  this.setState({FirstName: 'Morgan'});
	  this.setState({LastName: 'Cheng'});
	}
```

等到負責處理佇列的任務要處理時，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其狀態值會狀態修改合併後的樣子，也就是同時指定修改FirstName和LastName的一個任務，最後就這個任務來觸發updating的生命週期
```
	function updateName() {
	  this.setState({FirstName: 'Morgan', LastName: 'Cheng'});
	}
```



## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]
References:
[[@gaearonAutomaticBatchingFewer]]
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]