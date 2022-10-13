## 描述

componentDidMount 只會執行一次
componentDidUpdate 會執行多次
componentWillUnmount 只會執行一次



### 當前端索要後端資源並渲染
當要指定索取渲染用的資料時，會在componentDidMount階段進行
```
1.  componentDidMount() {
2.     // send http request
3.     this.setState(response)
4.  }
```


### useEffect 在class-based component 的實現



由於useEffect 本身就是componentDidUpdate、componentDidMount、componentWillUnmount 階段被執行，所以若要在class-based component實現useEffect，就要在每個元件的各個內建函式下定義對應的effect：
	- componentDidMount
	- componentDidUpdate
	- componentWillUnmount


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


  

主要是根據更新前的資訊來執行更新後所要做的事情

1.  componentDidUpdate(prevProps, prevState, snapshot)

- prevProps ：更新前的props資訊

- preState：更新前的state 資訊

  

  

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


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React componentDidUpdate 是每個元件都會有的內建生命週期函式，最主要是定義渲染內容更新後要做什麼]]
References: