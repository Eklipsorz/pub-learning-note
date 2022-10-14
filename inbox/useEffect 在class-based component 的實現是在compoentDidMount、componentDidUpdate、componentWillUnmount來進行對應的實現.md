## 描述

componentDidMount 只會執行一次
componentDidUpdate 會執行多次
componentWillUnmount 只會執行一次



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


### useEffect 在class-based component 的實現

由於useEffect 本身就是componentDidUpdate、componentDidMount、componentWillUnmount 階段被執行，所以若要在class-based component實現useEffect，就要在每個元件的各個內建函式下定義對應的effect：
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
其解法為使用componentDidUpdate內建函式所提供的preProps、prevState來比較更新前的資訊和更新後的資訊是否一致來實現useEffect的dependency功能

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
由於該函式因為unmount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect下的cleanup


## 複習


#🧠 當前端索要後端資源並渲染，那麼在class-based component的實現方式是？ ->->-> `在對應元件下的componentDidMount內建的函式中添加 發送請求和根據請求結果來執行setState`
<!--SR:!2022-10-17,3,250-->

#🧠 當前端索要後端資源並渲染，那麼在functional component的實現方式是？ ->->-> `在對應元件的component function下添加useEffect，並於useEffect的callback中添加發送請求和根據請求結果來執行setState1`
<!--SR:!2022-10-17,3,250-->


#🧠 functional component 所能使用的useEffect 在class-based component 的實現會是什麼？ ->->-> ` componentDidMount 函式： 由於該函式因為Mount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect；若effect 本身會是觸發渲染函式，那麼勢必會遇到無限迴圈的問題，所以通常會添加條件式、執行cleanup、執行effect`

#🧠 functional component 所能使用的useEffect 在class-based component 的實現會是什麼？ 以componentDidMount函式來說 ->->-> `componentDidMount 函式： 由於該函式因為Mount而執行，所以不會遇到無限迴圈的問題，通常實現方式是直接執行對應effect`
<!--SR:!2022-10-17,3,250-->


#🧠 functional component 所能使用的useEffect 在class-based component 的實現會不會在componentDidMount遇上無限循環問題？為什麼->->-> `不會，具體是由於Mount只會因為元件對應DOM被安裝至DOM Tree才執行，若因為componentDidMount內有setState而執行渲染函式，其階段也會由於處於updating階段而不會執行omponentDidMount`


#🧠 functional component 所能使用的useEffect 在class-based component 的實現會不會在componentWillUnmount遇上無限循環問題？為什麼->->-> `不會，具體是由於Mount只會因為從DOM Tree移除對應DOM才執行，若因為componentWillUnmount內有setState而執行渲染函式，其階段也會由於處於updating階段而不會執行componentWillUnmount`
<!--SR:!2022-10-17,3,250-->

#🧠 functional component 所能使用的useEffect 在class-based component 的實現會不會在componentDidUpdate遇上無限循環問題？為什麼->->-> `會，因為若componentDidUpdate裡頭有setState而執行，其階段由於還處於updating階段而繼續執行componentDidUpdate，繼而演變成進入渲染週期->進入componentDidUpdate執行setState的無限循環`
<!--SR:!2022-10-18,3,250-->

#🧠 functional component 所能使用的useEffect 在class-based component 的實現在componentDidUpdate遇上無限循環問題，解法會是->->-> `在裡頭添加類似dependency的條件式就能解決`
<!--SR:!2022-10-18,3,250-->


#🧠 componentDidMount、componentDidUpdate、componentWillUnmount 在正常情況下(mount->update->update->unmount)的執行次數會是如何 ->->-> `1、2、1`
<!--SR:!2022-10-17,3,250-->


#🧠 以下為React的class-base component，請問以下程式碼有何潛在問題？如何解決![https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-problem_tnvw8x.png](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-problem_tnvw8x.png) ->->-> `具有無限迴圈的潛在問題。![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1665664892/blog/react/life-cycle/componentDidUpdate/componentDidUpdate-loop-solution_fivxhx.png)`


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼]]
References: