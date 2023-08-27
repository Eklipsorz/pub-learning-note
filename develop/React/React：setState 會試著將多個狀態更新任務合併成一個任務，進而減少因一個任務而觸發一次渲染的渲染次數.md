


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

### class-based component vs. functional component ： state  & setState

在同個元件下，每個setState會是：
1. state 註冊範疇：class-based component 的 單個state 註冊元件下的所有狀態；functional component 的 單個state 註冊元件下的一個特定狀態
2. setState 註冊範疇：class-based component 的 單個setState 負責元件下的所有狀態之更新；functional component 的 單個setState  原則元件下的一個特定狀態之更新
3. setState 更新狀態方式：class-based component 的 單個setState 更新方式會是先以前一個狀態為基礎來增加額外狀態成為裡頭的子狀態或者覆蓋狀態內的子狀態；functuonal component 的 單個setState 更新狀態方式會是直接覆蓋前一個setState狀態或者前一個狀態



### 實際實現 1 - 將狀態更新任務放置佇列

- setState **每一次呼叫時，會生成非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染** 
- 在class-based component中的batching實際實現：由於因為語法限制而只能時常以物件來包含元件下的所有屬性，也有可能只有一個狀態且狀態值是單一值
	- 若狀態是以單一值來儲存的話，就直接拿目前任務的請求狀態去覆蓋先前任務所記錄的狀態
	- 若狀態是以多屬性的物件來儲存的話
		- 一開始會定義結果狀態為空物件
		- 將setState設定的狀態(物件的屬性)去追加/覆蓋至結果狀態物件上的屬性
			- 若要求更改狀態的屬性並沒有存在結果狀態物件的屬性中，直接增加該屬性至結果狀態物件
			- 若要求更改狀態的屬性存在結果狀態物件的屬性中，就直接以目前要求更改的狀態覆蓋至結果物件上的相對應屬性
- 在functional component中的batching實際實現：每種狀態都有各自狀態更新用的函式，每個由useState所註冊的狀態會被視為結果狀態物件中的一種屬性
	- 一開始會定義結果狀態為空物件：
		- 若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，直接增加該屬性至結果狀態物件
		- 若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，就直接以目前要求更改的狀態覆蓋至結果物件上的相對應屬性

		

### 實際實現 2 - 處理佇列的任務

**當非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期** 

- 實際實現為：當目前可以合併的指令都完成合併時，就執行
	- 以目前結果狀態來觸發實際狀態更新 & 渲染。



#### class-based component 案例 1
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

#### class-based component 案例 2

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


#### functional component 案例1
以class-based component為參考案例，所對應的語法會是如下
```
const [firstName, setFirstName] = useState('');
const [lastName, setLastName] = useState('');
```

使用兩次useState來註冊兩種狀態分別為firstName、lastName，當執行以下setState時
```
setFirstName('Morgan');
setLastName('Cheng');
```

執行前會先設定空物件為結果狀態物件
```
{}
```

接著執行第一個setState-setFirstName時，其狀態物件會是
```
// 追加後
{ FirstName: 'Morgan' }
```

然後再執行第二個setState-setLastName時，其狀態物件會是
```
// 追加前 
{ FirstName: 'Morgan' }
// 追加後
{ FirstName: 'Morgan', LastName: 'Cheng' }
```


做完發現沒了，就直接讓負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染


### useState 何時觸發執行？
[[@vencovskyAnswerWhenUse2019]]

> useCallback
> On every render, everything that's inside a functional component will run again.

重點：
- 每一次執行元件的render函式就會執行useState，首次mount階段會以初始值來表示，update階段則是會以新狀態來回傳





## 複習

#🧠 React：無論是否為class-based componet 或者 functional component，setState 每一次執行時，概念會如何執行 ->->-> `會生成以下指定任務內容的非同步任務並放進佇列，其佇列會給系統中的非同步任務X來負責處理渲染，指定任務內容為更新指定狀態值，當沒有再度接收setState時，非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期`
<!--SR:!2023-06-17,154,250-->

#🧠 React：在class-based component中的batching實際實現中， setState 的狀態是以單一值或者primitive data value，會如何進行狀態的batching？->->-> `若狀態是以單一值來儲存的話，就直接拿目前任務的請求狀態去覆蓋先前任務所記錄的狀態`
<!--SR:!2023-08-11,192,250-->


#🧠 React： 在class-based component中的batching實際實現中， setState 的狀態是以物件，會如何進行狀態的batching？ ->->-> `一開始會定義結果狀態為空物件、將setState設定的狀態(物件的屬性)去追加/覆蓋至結果狀態物件上的屬性`
<!--SR:!2024-12-26,494,250-->

#🧠 React：無論狀態更新是否為class-based componet 或者 functional component，有誰能夠執行完setState便立刻更新state嗎 ->->-> `都沒有`
<!--SR:!2023-08-10,191,250-->


#🧠 React：無論是否為class-based componet 或者 functional component，請問setState 每一次呼叫時會立刻更新state嗎？ 為何？->->-> `並不會，具體要等所有狀態更新指令執行完畢，並且以batching形式來合併狀態，最後以最後合併狀態為結果狀態來進行一次狀態更新和出發渲染週期`
<!--SR:!2024-12-27,495,250-->

#🧠 React：setState1(A) setState2(B) setState3(C)，請問最後的batching結果會是什麼 ->->-> `會是個{state1: A, state2: B, state3: C}的結果，並以這個狀態來更新狀態和觸發渲染`
<!--SR:!2023-08-09,190,250-->


#🧠 React：setState1(A) setState2(B) setState1(A1) ，請問最後的batching結果會是什麼->->-> `會是個{state1: A1, state2: B}的結果，並以這個狀態來更新狀態和觸發渲染`
<!--SR:!2023-08-13,193,250-->





#🧠 React： **當非同步任務X開始處理佇列裡的非同步任務，會先將佇列裡的任務們所要求的狀態修改合併，這會使得多個任務合併成一個任務，其任務要求指定的狀態值會是多個任務所指定的狀態所合併的樣子，最後就以那個任務來觸發updating的生命週期** ，其實際實現為何？ ->->-> `實際實現為：當目前可以合併的指令都完成合併時，就執行以目前結果狀態來觸發實際狀態更新 & 渲染。`
<!--SR:!2023-06-25,192,250-->


#🧠 React：在class-based componet中，負責處理儲存多個狀態更新任務佇列的非同步任務X何時會做狀態更新&渲染 ->->-> `等到沒有狀態更新任務可被執行，就開始執行`
<!--SR:!2024-07-31,394,250-->

#🧠 React：在functional component中，負責處理儲存多個狀態更新任務佇列的非同步任務X何時會做狀態更新&渲染 ->->-> `等到沒有狀態更新任務可被執行，就開始執行`
<!--SR:!2023-07-08,168,250-->



#🧠 React18：class-based component 假如系統執行以下setState，而狀態會是以單一值來表示，那麼過程會是如何執行狀態更新![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-value-example_tw7yp7.png) ->->-> `執行第一個this.setState指令任務，會先將結果物件設定為 2、執行第二個this.setState指令任務，會先將結果物件設定為 3、執行第三個this.setState指令任務，會先將結果物件設定為 4、做完發現沒了，就直接負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染`
<!--SR:!2024-12-28,496,250-->


#🧠 React18：class-based component 假如系統執行以下setState，而狀態會是以物件來表示，那麼過程會是如何執行狀態更新![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `執行第一個this.setState指令任務，會先將結果物件設定為空物件，並將該任務要求更改的狀態值追加至空物件，做完就做第二個。執行第二個this.setState指令任務，會先將任務要求更改的狀態追加/覆蓋至空物件，做完就看有沒有第三個。做完發現沒了，就直接讓負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染`
<!--SR:!2023-06-01,143,250-->

#🧠 若透過以下語法而獲得\{ FirstName: \'Morgan\', LastName: \'Cheng\' \}，請問是屬於哪種元件開發方法？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `class-based component`
<!--SR:!2024-08-04,398,250-->


#🧠 React：setState1(\{firstName: \'Morgan\' \}); setState1(\{lastName:\'Cheng\'\}) 請問最後結果會是什麼？為什麼->->-> `最後結果為{lastName: 'Cheng'}，因為這是functional component，而setState1則是對於同一個狀態的狀態更新函式，換言之，就是同一個狀態，所以這對於batching的結果狀態物件來說，只是對同一種屬性的覆寫`
<!--SR:!2023-08-02,185,250-->






#🧠 React18：class-based component 假如系統執行以下setState，而狀態會是以單一值來表示，那麼會以何種狀態來渲染和更新狀態？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-value-example_tw7yp7.png) ->->-> `4`
<!--SR:!2024-11-08,493,250-->

#🧠 React18：class-based component 假如系統執行以下setState，而狀態會是以物件來表示，那麼會以何種狀態來渲染和更新狀態![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `{ FirstName: 'Morgan', LastName: 'Cheng' }`
<!--SR:!2023-06-18,187,250-->


#🧠 React useState 何時觸發執行？ ->->-> `每一次執行元件的render函式就會執行useState`
<!--SR:!2024-12-03,476,250-->

#🧠 React useState 每次觸發執行所回傳的狀態會是？ ->->-> `首次mount階段會以初始值來表示，update階段則是會以新狀態來回傳`
<!--SR:!2023-10-01,193,230-->

#🧠 React：在functional component中的batching實際實現是如何進行batching?->->-> `每種狀態都有各自狀態更新用的函式，所以會以每個由useState所註冊的狀態視為結果狀態物件中的一種屬性，接著執行setState之前，一開始會定義結果狀態為空物件，- 若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，直接增加該屬性至結果狀態物件 - 若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，就直接以目前要求更改的狀態覆蓋至結果物件上的相對應屬性`
<!--SR:!2023-08-12,192,250-->

#🧠 React：在functional component中的batching實際實現下，剛開始執行batching時，系統會做什麼？ ->->-> `一開始會定義結果狀態為空物件`
<!--SR:!2023-11-07,130,210-->

#🧠 React：在functional component中的batching實際實現下，一開始剛開始執行batching會定義結果狀態為空物件並根據狀態的屬性是否存在來處理，請問這是什麼意思？->->-> `就是按照每個被註冊的狀態來當作屬性來納入結果狀態物件上`
<!--SR:!2024-12-21,490,250-->

#🧠 React：在functional component中的batching實際實現是如何進行batching，一開始會定義結果狀態為空物件，接著根據狀態的屬性是否存在來處理，那麼如何做？>->-> `若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，直接增加該屬性至結果狀態物件、 若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，就直接以目前要求更改的狀態覆蓋至結果物件上的相對應屬性`

#🧠 React：在functional component中的batching實際實現是如何進行batching，一開始會定義結果狀態為空物件，接著根據狀態的屬性是否存在來處理，若要求更改狀態的屬性本身並沒有存在結果狀態物件的屬性中，那接下來如何做？ ->->-> `直接增加該屬性至結果狀態物件`
<!--SR:!2023-08-08,189,250-->

#🧠 React：在functional component中的batching實際實現是如何進行batching，一開始會定義結果狀態為空物件，接著根據狀態的屬性是否存在來處理，若要求更改狀態的屬性本身並存在結果狀態物件的屬性中，那接下來如何做？->->-> `就直接以目前要求更改的狀態覆蓋至結果物件上的相對應屬性`
<!--SR:!2024-12-08,469,250-->


#🧠 請試著以functional component的方式來打造以下的狀態batching![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661180158/blog/react/batching/handler-multiple-setState-object-example_lcz6tg.png) ->->-> `const [firstName, setFirstName] = useState('');、const [lastName, setLastName] = useState('');、setFirstName('Morgan');setLastName('Cheng');`
<!--SR:!2023-08-14,194,250-->

#🧠 React：setFirstName('Morgan'); setLastName('Cheng'); 是屬於哪一種元件開發方法？ ->->-> `functional component`
<!--SR:!2024-07-29,395,250-->

#🧠 React：setFirstName('Morgan'); setLastName('Cheng'); 請問如何做狀態的batching？ ->->-> `當執行以下setState時，執行前會先設定空物件為結果狀態物件 {}，接著執行第一個setState-setFirstName時，其狀態物件會是{ FirstName: 'Morgan' }，然後再執行第二個setState-setLastName時，其狀態物件會是{ FirstName: 'Morgan', LastName: 'Cheng' }，做完發現沒了，就直接讓負責處理佇列的非同步任務X來對夾帶著特定狀態值的合併後任務進行狀態更新&渲染`
<!--SR:!2024-12-06,479,250-->


#🧠 class-based component vs. functional component ： state  & setState 有哪些主要差別(簡要就好) ->->-> `state 註冊範疇、setState 註冊範疇、setState 更新狀態方式`
<!--SR:!2023-07-04,167,250-->

#🧠 class-based component vs. functional component ： state  & setState 在 單個state 註冊範疇是什麼？說明清楚 ->->-> `class-based component 的 單個state 註冊元件下的所有狀態；functional component 的 單個state 註冊元件下的一個特定狀態`
<!--SR:!2023-08-10,191,250-->


#🧠 class-based component vs. functional component ： state  & setState 對於在 單個state 註冊範疇之差別是什麼？說明清楚 ->->-> `class-based component 的 單個state 註冊元件下的所有狀態；functional component 的 單個state 註冊元件下的一個特定狀態`
<!--SR:!2023-12-04,99,230-->


#🧠 class-based component vs. functional component ： state  & setState 對於在單個setState 註冊範疇之差別 是什麼？說明清楚 ->->-> `class-based component 的 單個setState 負責元件下的所有狀態之更新；functional component 的 單個setState  原則元件下的一個特定狀態之更新`
<!--SR:!2023-11-25,90,230-->

#🧠 class-based component vs. functional component ： 單個 state  & setState 對於單個setState 更新狀態方式之差別 是什麼？ (提示子狀態、以什麼為主來延伸)說明清楚 ->->-> `class-based component 的 單個setState 更新方式會是先以前一個狀態為基礎來增加額外狀態成為裡頭的子狀態或者覆蓋狀態內的子狀態；functuonal component 的 單個setState 更新狀態方式會是直接覆蓋前一個setState狀態或者前一個狀態`
<!--SR:!2023-08-13,193,250-->

#🧠 class-based component vs. functional component ： 單個 state  &  setState 對於單個setState 更新狀態方式之差別 是什麼？ 說明清楚 ->->-> `class-based component 的 單個setState 更新方式會是先以前一個狀態為基礎來增加額外狀態成為裡頭的子狀態或者覆蓋狀態內的子狀態；functuonal component 的 單個setState 更新狀態方式會是直接覆蓋前一個setState狀態或者前一個狀態`
<!--SR:!2023-09-16,185,230-->

---
Status: #☀️ 
Tags:
[[React]] - [[JavaScript]]
Links:
[[class-based component 的狀態通常會以物件來囊括元件下的所有狀態，而functional component的狀態透過useState可以建立多個獨立的狀態，而非集中在物件上]]
[[React batching 是將N個狀態更新指令合併成一個指令並只引發一次畫面渲染]]
References:
[[@gaearonAutomaticBatchingFewer]]
[[@chengmomorganSetStateZheGeAPISheJiDaoDiZenMeYang]]