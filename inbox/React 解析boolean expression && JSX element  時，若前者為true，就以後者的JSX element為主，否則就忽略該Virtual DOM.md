## 描述
### React 解析 boolean expression && jsx element
[[@reactTiaoJianRenderReact]]
```
function Mailbox(props) {
  const unreadMessages = props.unreadMessages;
  return (
    <div>
      <h1>Hello!</h1>
      {unreadMessages.length > 0 &&        <h2>          You have {unreadMessages.length} unread messages.        </h2>      }    </div>
  );
}

const messages = ['React', 'Re: React', 'Re:Re: React'];

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<Mailbox unreadMessages={messages} />);
```

> 能夠這樣做是因為在 JavaScript 中，`true && expression` 總是回傳 `expression` ，而 `false && expression` 總是回傳 `false`。

> 所以，當條件為 `true` 時，`&&` 右側的 element 會出現在輸出中，如果是 `false`，React 會忽略並跳過它。


重點：
- React 解析boolean expression && jsx element  時：
	- 若表達前者是回傳true，就會以後者的 JSX Element來呈現
	- 若表達前者是回傳false，React就會選擇忽略該Virtual DOM
```
boolean expression && jsx element
```

### boolean expression && JSX element 適用場景

該語法只會在該元件本身就為boolean expression && JSX element 
```
return (
	result && <ErrorModal onErrorModal={onErrorModalClickHandler}></ErrorModal>
);
```


## 複習


---
Status: #🌱 #📓 
Tags:
[[React]] 
Links:
[[React：conditional rendering 是根據執行狀態來調整渲染內容的技術]]
References:
[[@reactTiaoJianRenderReact]]