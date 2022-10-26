## 描述


### 解決前

事件處理是使用到this，但這個this還是得取決於函式呼叫時的this是什麼？
```
  toggleUsersHandler() {
    this.setState((prevState) => ({
      showUsers: !prevState.showUsers,
    }));
  }
```

在這裡由於未對toggleUsersHandler的函式呼叫做特別的this綁定，導致該函式的this會是設定發生事件的DOM節點。
```
return (
	<button onClick={this.toggleUsersHandler}>
)
```


```
import { useState, Component } from 'react';
import User from './User';

import classes from './Users.module.css';

const DUMMY_USERS = [
  { id: 'u1', name: 'Max' },
  { id: 'u2', name: 'Manuel' },
  { id: 'u3', name: 'Julie' },
];

class Users extends Component {
  constructor() {
    super();
    this.state = { showUsers: true, more: 'hi' };
  }

  toggleUsersHandler() {
    this.setState((prevState) => ({
      showUsers: !prevState.showUsers,
    }));
  }

  render() {
    const usersList = (
      <ul>
        {DUMMY_USERS.map((user) => (
          <User key={user.id} name={user.name} />
        ))}
      </ul>
    );
    console.log('state', this.state.showUsers, this.state.more);
    return (
      <div className={classes.users}>
        <button onClick={this.toggleUsersHandler}>
          {this.state.showUsers ? 'Hide' : 'Show'} Users
        </button>
        {this.state.showUsers && usersList}
      </div>
    );
  }
}

export default Users;

```

### 解決後
```
import { useState, Component } from 'react';
import User from './User';

import classes from './Users.module.css';

const DUMMY_USERS = [
  { id: 'u1', name: 'Max' },
  { id: 'u2', name: 'Manuel' },
  { id: 'u3', name: 'Julie' },
];

class Users extends Component {
  constructor() {
    super();
    this.state = { showUsers: true, more: 'hi' };
  }

  toggleUsersHandler() {
    this.setState((prevState) => ({
      showUsers: !prevState.showUsers,
    }));
  }

  render() {
    const usersList = (
      <ul>
        {DUMMY_USERS.map((user) => (
          <User key={user.id} name={user.name} />
        ))}
      </ul>
    );
    console.log('state', this.state.showUsers, this.state.more);
    return (
      <div className={classes.users}>
        <button onClick={this.toggleUsersHandler.bind(this)}>
          {this.state.showUsers ? 'Hide' : 'Show'} Users
        </button>
        {this.state.showUsers && usersList}
      </div>
    );
  }
}

export default Users;
```

## 複習

#🧠 在React中的class-based component中，渲染部分設定成這樣\<button onClick=\{this.toggleUsersHandler\}\>，且toggleUsersHandler內部含有this.setState，請問若直接讓按鈕發生點擊事件，會是如何？ ->->-> `其中this會是以發生事件的dom節點來執行，但該節點別沒有setState而報錯`

#🧠 在React中的class-based component中，渲染部分設定成這樣\<button onClick=\{this.toggleUsersHandler\}\>，且toggleUsersHandler內部含有this.setState，請問若直接讓按鈕發生點擊事件，會是this會是以發生事件的dom節點來執行，如何解決？->->-> `對該函式進行bind來綁定this為對應元件類別的物件，this.toggleUsersHandler.bind(this)`

---
Status: #🌱 
Tags:
[[React]]
Links:
References: