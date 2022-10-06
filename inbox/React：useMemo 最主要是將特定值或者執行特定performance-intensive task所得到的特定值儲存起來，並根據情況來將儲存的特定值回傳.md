## 描述

[[@ithomeDay8ReactHookPianRenShi]]
> `const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);`

> -   第一個參數是 callback function
> -   第二個參數是一個陣列，此陣列不作為傳到 callback function 的參數
>    -   `useMemo(computation)`: 如果沒有加上這個陣列，每次都會重新執行函式去產生新的值
>    -   `useMemo(computation, [])`: 空陣列的話，回傳值不會改變
>    -   `useMemo(computation, [...someValues])`: 有加上一些元素值的話，當元素值改變時會重新更新函式回傳值


[[@reactHooksAPICanKao]]
```
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

> 回傳一個 memoized 的值。

> 傳遞一個「建立」function 及依賴 array。useMemo 只會在依賴改變時才重新計算 memoized 的值。這個最佳化可以避免在每次 render 都進行昂貴的計算。


重點：
- useMemo 最主要是將特定值或者執行特定performance-intensive task所得到的特定值儲存起來，並根據情況來將儲存的特定值回傳或者重新執行performance-intensive task來獲得特定值
- useMemo 語法為如下
	- 第一個參數為專門定義所要儲存的結果值，會以函式物件來表示如何產生對應的結果值
		- 函式物件得要有return 特定值的手段，若沒有添加會以undefine為回傳結果
	- 第二個參數為依賴項目所構成的陣列，會依據：
		- deps 若為空陣列的話，系統就認為不會有任何變動的deps，並且只回傳記憶體的目前內容，不執行createResultFn來產生
		- deps 若沒設定的話，系統就認為會是一直變動的deps，並且會執行createResultFn來得到其回傳值，接著用回傳值來儲存在記憶體中。
		- deps 若設定為\[a, b\]的話，系統就以a、b來決定是否回傳記憶體的內容，若任一變動，就執行createResultFn來得到其回傳值，接著用回傳值來儲存在記憶體中；若沒變動，就回傳記憶體的內容
```
const memoizedValue = useMemo(createResultFn, [deps]);
```
#### 案例1

假設有個App.js，預期它會渲染出特定幾個數字排列後的清單，該元件夾雜著DemoList 和 Button 這兩個元件，在這裡App元件會賦予一系列沒排列好的數字給DemoList元件來排序並要求它呈現最後排序後的樣子。

在這裡可以改善的效能是：
- DemoList中的排序功能能夠依據數字清單是否相同來決定執行：若相同就回傳先前結果，而不執行；若不相同就執行並回傳執行結果

然後實際上若直接在DemoList.js使用useMemo並以items作為deps，會因為每次接收到的items記憶體位址而不同，沒辦法以記憶體儲存的結果來回傳，換言之，沒使用到useMemo的正常好處

```
  const sortedList = useMemo(() => {
    console.log('Items sorted');
    return items.sort((a, b) => a - b);
  }, [items]); 
```

```
import React, { useState, useCallback } from 'react';

import './App.css';
import DemoList from './components/Demo/DemoList';
import Button from './components/UI/Button/Button';

function App() {
  const [listTitle, setListTitle] = useState('My List');

  const changeTitleHandler = useCallback(() => {
    setListTitle('New Title');
  }, []);

  return (
    <div className='app'>
      <DemoList title={listTitle} items={[5, 3, 1, 10, 9]} />
      <Button onClick={changeTitleHandler}>Change List Title</Button>
    </div>
  );
}

export default App;
```

DemoList.js 元件
```
import React, { useMemo } from 'react';

import classes from './DemoList.module.css';

const DemoList = (props) => {
  const { items } = props;

  const sortedList = useMemo(() => {
    console.log('Items sorted');
    return items.sort((a, b) => a - b);
  }, [items]); 
  console.log('DemoList RUNNING');

  return (
    <div className={classes.list}>
      <h2>{props.title}</h2>
      <ul>
        {sortedList.map((item) => (
          <li key={item}>{item}</li>
        ))}
      </ul>
    </div>
  );
};

export default React.memo(DemoList);
```


#### 案例2

### useMemo 所儲存的記憶體區塊內容為何
最主要會是以原本識別字所對應的stack記憶體區塊內容為主：
- 若為物件的話，就以物件的識別字來找到stack記憶體區塊，並以區塊內容中的reference value來比較
- 若為primitivie data value，就以識別字來找到stack記憶體區塊，並以區塊內容的primitive data value 來比較

### useMemo 適用場景為
- 經由複雜計算才能夠獲取到的內容，或者執行performance-intensive才能獲得的內容
- props以非函式的物件為內容的元件並納入使用memo，由於物件會因為渲染函式而重造並得到不同的記憶體位址，而無法正常使用memo的功能


###  useMemo 什麼時候執行觸發
[[@reactHooksAPICanKao]]
> 要謹記傳到 `useMemo` 的 function 會在 render 期間執行。不要做一些通常不會在 render 期間做的事情。例如，處理 side effect 屬於 `useEffect`，而不是 `useMemo`。

重點：
- useMemo 在對應元件的render function執行時，才會被執行

## 複習

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``



---
Status: #🌱 
Tags:
Links:
References:
[[@ithomeDay8ReactHookPianRenShi]]
[[@reactHooksAPICanKao]]