## 描述




### 當前端索要後端資源並渲染

#### 在class-based component
當要指定索取渲染用的資料時，會在componentDidMount階段進行
```
1.  componentDidMount() {
2.     // send http request
3.     this.setState(response)
4.  }
```

#### 在functional component

```
useEffect(() => {
	// send http request 
	setState1(....)
})
```


### useEffect 本身並不是class-based component的實現或者語法糖

嚴格來說只是兩者採用同個react核心代碼來以兩種截然不同的形式來實現兩個獨立功能

### 在class-based component 的實現來模擬useEffect

若要在class-based component 的實現來模擬useEffect，會用到以下生命週期函式：
- componentDidMount：無視dependency並執行effect 
- componentDidUpdate：根據dependency是否變動來執行cleanup -> effect
- componentWillUnmount：無視dependency並執行cleanup

#### componentDidMount
由於該函式因為Mount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect

#### componentDidUpdate
若effect 本身會是觸發渲染函式，那麼勢必會遇到無限迴圈的問題：
	- 進入渲染週期，並執行到componentDidUpdate
	- 執行effect內的觸發渲染函式
	- 進入渲染週期，並執行到componentDidUpdate
	- 執行effect內的觸發渲染函式
	- .....
其解法為使用componentDidUpdate內建函式所提供的prevProps、prevState來比較更新前的資訊和更新後的資訊是否一致來實現useEffect的dependency功能

##### 案例1：
```
1.  componentDidUpdate() {
2.       this.setState({
3.            filteredUsers: DUMMY_USERS.filter((user) => 
4.                 user.name.includes(this.state.searchTerm)
5.            )
6.       })
7.  }
```

潛在問題為：
- 引發無限迴圈問題，理由為該effect為觸發渲染函式的effect


解法為
- 設定一個條件來觸發：當關注的狀態有變動時就觸發
```
1.  componentDidUpdate(prevProps, prevState) {
2.      if (prevState.searchTerm !== this.state.searchTerm) {
3.       this.setState({
4.            filteredUsers: DUMMY_USERS.filter((user) => 
5.                 user.name.includes(this.state.searchTerm)
6.            )
7.       })
8.     }
9.  }
```
  
#### componentWillUnmount
具體是由於Mount只會因為從DOM Tree移除對應DOM才執行，若因為componentWillUnmount內有setState而執行渲染函式，其階段也會由於處於updating階段而不會執行componentWillUnmount，但之後肯定會遇到unmount階段來釋放，所以又會執行一次componentWillUnmount


## 複習


#🧠 React：由於可以在class-based component的componentDidMount、componentDidUpdate、componentWillUnmount來實現useEffect的功能，我們可以說useEffect就是他們的語法糖嗎 ->->-> `並不能，兩者為獨立功能`
<!--SR:!2023-02-02,53,250-->

#🧠 React：若要在class-based component 實現 useEffet會有的功能，會用上什麼函式 ->->-> `componentDidMount、componentDidUpdate、componentWillUnmount`
<!--SR:!2023-03-02,72,250-->

#🧠 React：useEffect 本身是class-based component 的 componentDidMount、componentDidUpdate、componentWillUnmount這三者的語法糖？為什麼？->->-> `並不是，嚴格來說只是兩者採用同個react核心代碼來以兩種截然不同的形式來實現兩個獨立功能`
<!--SR:!2023-03-04,74,250-->


#🧠 React：當前端索要後端資源並渲染，那麼在class-based component的實現方式是？ ->->-> `在對應元件下的componentDidMount內建的函式中添加 發送請求和根據請求結果來執行setState`
<!--SR:!2023-01-26,67,250-->

#🧠 React：當前端索要後端資源並渲染，那麼在functional component的實現方式是？ ->->-> `在對應元件的component function下添加useEffect，並於useEffect的callback中添加發送請求和根據請求結果來執行setState1`
<!--SR:!2023-01-25,66,250-->


#🧠 React：若要在class-based component 去實現useEffect會是什麼？ ->->-> ` componentDidMount 函式： 由於該函式因為Mount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect；若effect 本身會是觸發渲染函式，那麼勢必會遇到無限迴圈的問題，所以通常會添加條件式、執行cleanup、執行effect`
<!--SR:!2023-02-25,69,250-->


#🧠 React：若要在class-based component 去實現useEffect會是什麼？以componentDidMount函式來說 ->->-> `componentDidMount 函式： 由於該函式因為Mount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect`
<!--SR:!2023-02-05,73,250-->


#🧠 React：若要在class-based component 去實現useEffect會是什麼：在class-based component 的實現會不會在componentDidMount遇上無限循環問題？為什麼->->-> `不會，具體是由於Mount只會因為元件對應DOM被安裝至DOM Tree才執行，若因為componentDidMount內有setState而執行渲染函式，其階段也會由於處於updating階段而不會執行omponentDidMount`
<!--SR:!2023-03-04,74,250-->



#🧠 React：若要在class-based component 去實現useEffect會是什麼：在class-based component 的實現會不會在componentWillUnmount遇上無限循環問題？為什麼->->-> `會，具體是由於Mount只會因為從DOM Tree移除對應DOM才執行，若因為componentWillUnmount內有setState而執行渲染函式，其階段也會由於處於updating階段而不會執行componentWillUnmount，但之後肯定會遇到unmount階段來釋放，所以又會執行一次componentWillUnmount`
<!--SR:!2023-02-05,52,250-->



#🧠  React：若要在class-based component 去實現useEffect會是什麼：functional component 所能使用的useEffect 在class-based component 的實現會不會在componentDidUpdate遇上無限循環問題？為什麼->->-> `會，因為若componentDidUpdate裡頭有setState而執行，其階段由於還處於updating階段而繼續執行componentDidUpdate，繼而演變成進入渲染週期->進入componentDidUpdate執行setState的無限循環`
<!--SR:!2023-03-04,74,250-->


#🧠  React：若要在class-based component 去實現useEffect會是什麼： 在class-based component 的實現在componentDidUpdate遇上無限循環問題，解法會是->->-> `在裡頭添加類似dependency的條件式就能解決`
<!--SR:!2023-03-04,74,250-->

#🧠 React：componentDidUpdate(prevProps, prevState)的prevProps, prevState會是指什麼？ ->->-> `更新前的props資訊和更新前的state`
<!--SR:!2023-01-07,3,250-->


#🧠 componentDidMount、componentDidUpdate、componentWillUnmount 在正常情況下(mount->update->update->unmount)的執行次數會是如何 ->->-> `1、2、1`
<!--SR:!2023-02-06,74,250-->


#🧠 以下為React的class-base component，請問以下程式碼有何潛在問題？如何解決![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-problem_tnvw8x.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-problem_tnvw8x.png) ->->-> `具有無限迴圈的潛在問題。![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-solution_fivxhx.png)`
<!--SR:!2023-02-04,72,250-->


---
Status: #🌱 
Tags:
[[React]] - [[useEffect]]
Links:
[[React componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼]]
[[side effect 是指調用者執行特定操作或表達式或函式而得到除了回傳值給調用者這個主要效果以外的額外效果，side effect 通常會是影響主調用者所使用的共享資源之效果]]
[[React：Effect 等同於 Side Effect，effect 本身是指執行主要處理(結果)所帶來的任意額外處理(結果)，主要處理(結果)會是指元件渲染(render)任務。任意額外處理(結果)指useEffect所定義的執行處理]]
References: