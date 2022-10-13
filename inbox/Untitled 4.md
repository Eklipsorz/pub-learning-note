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
由於該函式因為Mount通常

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
  

## 複習


#🧠 當前端索要後端資源並渲染，那麼在class-based component的實現方式是？ ->->-> `在對應元件下的componentDidMount內建的函式中添加 發送請求和根據請求結果來執行setState`

#🧠 當前端索要後端資源並渲染，那麼在functional component的實現方式是？ ->->-> `在對應元件的component function下添加useEffect，並於useEffect的callback中添加發送請求和根據請求結果來執行setState1`


#🧠 functional component 所能使用的useEffect 在class-based component 的實現會是什麼？ ->->-> `設定能夠阻止無限循環的`



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼]]
References: