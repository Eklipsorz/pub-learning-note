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


### 在渲染層級，能夠正常使用的場景

1. render 函式只回傳boolean expression && jsx element
```
return (
	boolean expression && jsx element
)
```

2. JSX 夾雜著{expresssion}，其中expression就填入boolean expression && jsx element


## 複習
#🧠 boolean expression && jsx element 在渲染層級上，哪些是能夠正常讓語法發揮正常用途的場景->->-> `render 函式只回傳boolean expression && jsx element、JSX 夾雜著{expresssion}，其中expression就填入boolean expression && jsx element`
<!--SR:!2022-09-21,8,250-->

#🧠 React 解析JSX 元素中的{expressio}的expression，此時的expression是boolean expression && jsx element ，請問 boolean expression && jsx element會如何運作？->->-> `若表達前者是回傳true，就會以後者的 JSX Element來呈現、若表達前者是回傳false，React就會選擇忽略該Virtual DOM`
<!--SR:!2022-09-13,3,250-->




---
Status: #🌱 
Tags:
[[React]] 
Links:
[[在渲染層面下，render 函式回傳的內容若單純添加boolean expression && JSX element 的話，會使其語法正常執行，反之在其基礎下添加其他元素的話，其語法會被視為字串和一般的React Element來看待]]
[[React：conditional rendering 是根據執行狀態來調整渲染內容的技術]]
[[boolean expression && JSX Element案例：混雜其他元件＋boolean expression && JSX Element 未放入到{} vs. 混雜其他元件＋boolean expression && JSX Element 放入到 {}]]
References:
[[@reactTiaoJianRenderReact]]