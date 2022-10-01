## 描述




### 執行效果

> so we call the function for the DemoOutput component.

> We call the function for the button component. That's why those child components are also re-executed and re-evaluated just because the parent component changed because they are part of the parent components, function body.

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664648962/blog/react/life-cycle/%E6%88%AA%E5%9C%96_2022-10-02_%E4%B8%8A%E5%8D%882.25.24_rmntcb.png)
若parent component是由多個child component 或者由多個descendant component 所組成，當component發生updating時：

- 不論child component/ descendant component是否因為狀態、context、props發生變動，都會因為處於同一個parent component的一部分而跟著一起觸發updating

- 然而child component/descendant component所對應的real dom 若單純依據著props、context、狀態而渲染，那real dom並不會有任何變化




#### 範例 1

```
function App() {
  const [showParagraph, setShowParagraph] = useState(false);

  console.log('APP RUNNING');

  const toggleParagraphHandler = () => {
    setShowParagraph((prevShowParagraph) => !prevShowParagraph);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={toggleParagraphHandler}>Toggle Paragraph!</Button>
    </div>
  );
}
```



```
import React from 'react';

const DemoOutput = (props) => {
  console.log('DemoOutput RUNNING');
  return <p>{props.show ? 'This is new!' : ''}</p>;
};

export default DemoOutput;
```

#### 範例 2


```
function App() {
  const [showParagraph, setShowParagraph] = useState(false);

  console.log('APP RUNNING');

  const toggleParagraphHandler = () => {
    setShowParagraph((prevShowParagraph) => !prevShowParagraph);
  };

  return (
    <div className="app">
      <h1>Hi there!</h1>
      <DemoOutput show={false} />
      <Button onClick={toggleParagraphHandler}>Toggle Paragraph!</Button>
    </div>
  );
}
```



```
import React from 'react';
import Wrapper from './Wrapper';
const DemoOutput = (props) => {
  console.log('DemoOutput RUNNING');
  return <Wrapper>{props.show ? 'This is new!' : ''}</Wrapper>;
};

export default DemoOutput;
```

```
import React from 'react';

const Wrapper = (props) => {
  console.log('Wrapper RUNNING');
  return <p>{props.children}</p>;
};

export default Wrapper;
```


### 潛在問題

由於以下執行狀況而發生一個效能浪費的結果：過多沒實際擁有最新內容的元件(function component)而被呼叫，且這些元件還會讓React去做diff 算法

  

若parent component是由多個child component 或者由多個descendant component 所組成，當component發生updating時：

- 不論child component/ descendant component是否因為狀態、context、props發生變動，都會因為處於同一個parent component的一部分而跟著一起觸發updating


## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: