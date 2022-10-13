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


### useEffect 在

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
Links:
References: