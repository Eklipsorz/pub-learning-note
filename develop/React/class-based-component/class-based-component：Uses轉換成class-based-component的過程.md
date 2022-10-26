## 描述




### 在constructor 註冊狀態

在這裡由於該類別繼承React.component這基本類別，且得自製constructor才能註冊狀態，所以得親自在constructor使用super來從React.component這類別建立對應物件來延伸，接著再來註冊狀態

```
class Users extends Component {
  constructor() {
    super();
    this.state = {
      showUsers: true,
    };
  }
  .
  .
  .
}
```


### 事件處理函式 和 按鈕事件綁定

事件處理函式為了避免不必要重複定義，而直接成為元件類別下的方法，接著綁定在button上onClick，但在這裡要考量到的是toggleUsersUser本身使用了this，而貿然直接將事件處理設定給button，會因為JS原生對於事件處理之this binding而將this設定成button，而非為整個Users元件，因此得用bind(this)來解決

```
class Users extends Component {
  constructor() {
	  ....
  }
  toggleUsersHandler() {
    this.setState((curState) => {
      return { showUsers: !curState.showUsers };
    });
  }

  render() {
    const usersList = (
      <ul>
        {DUMMY_USERS.map((user) => (
          <User key={user.id} name={user.name} />
        ))}
      </ul>
    );

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

#💻 請至/react-builder/question-review/class-based-component-question 領取題目，並到Users-to-class分支將Users.js轉換成class-based component，功能務必是一模一樣->->-> `https://github.com/academind/react-complete-guide-code/blob/13-class-based-cmp/code/03-working-with-state/src/components/Users.js`
<!--SR:!2022-11-23,28,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
References: