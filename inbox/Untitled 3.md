

## 描述

### props 比對方式：
其比對方式會是基於JS的 === operator
```
currProp === prevProp
```

- 若比較對象(識別字)是primitive data type(如字串、數字)，識別字就會被JS解析成對應內容
- 若比較對象(識別字)是物件，識別字就會被JS解析成物件的記憶體位置
[[JS：若識別字是對應著primitive data type的內容，會直接將識別字解析成其內容；若識別字是對應著物件，會直接將識別字解析成其物件所在的記憶體位址]]


### 案例：


```
import React, { useState } from 'react';

import Button from './components/UI/Button/Button';
import DemoOutput from './components/Demo/DemoOutput';
import './App.css';

function App() {
  const [showParagraph, setShowParagraph] = useState(false);
  console.log('APP RUNNING');

  const toggleParagraphHandler = () => {
    setShowParagraph((prevShowParagraph) => !prevShowParagraph);
  };

  return (
    <div className='app'>
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={toggleParagraphHandler}>Toggle Paragraph!</Button>
    </div>
  );
}

export default App;
```


```
import React from 'react';

import classes from './Button.module.css';

const Button = (props) => {
  console.log('Button RUNNING');
  return (
    <button
      type={props.type || 'button'}
      className={`${classes.button} ${props.className}`}
      onClick={props.onClick}
      disabled={props.disabled}
    >
      {props.children}
    </button>
  );
};

export default React.memo(Button);
```


```
APP RUNNING
Button RUNNING
```

重點：
- 在這裡預期是


每一次渲染函式呼叫都會如同正常函式，去分配記憶體來建立它會用到的變數和函式，在這裡它每次執行每次都生成新的事件處理函式，其函式本身是物件，所以會以記憶體位址的不同來區分是否不同，所以prop-checking會一直會保持著改變而不採用記憶體的內容


## 複習



---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React.memo 適用場景為不常變更的元件內容、規模較大的專案，不適用場景為時常變更的元件、props為基礎來重複使用的元件、規模較小的專案]]
[[React.memo 效能取決於儲存空間成本和計算成本，前者會是props數量、對應元件的Virtual DOM結構、其descendant component的Virtual DOM結構，後者會是props比對成本]]
[[React：React.memo 將特定props之指定元件A的對應Virtual DOM儲存在緩存或者記憶體中，並比較每一次渲染觸發時的props資訊是否和儲存記憶體的資訊一致，一致就用記憶體，不一致就執行function]]
[[primitive data type 是指 電腦環境本身帶有的資料型別，而非程式語言會衍生的，該型別可以在程式語言下，組合成新的資料型別，如物件]]
[[JS：若識別字是對應著primitive data type的內容，會直接將識別字解析成其內容；若識別字是對應著物件，會直接將識別字解析成其物件所在的記憶體位址]]
References: