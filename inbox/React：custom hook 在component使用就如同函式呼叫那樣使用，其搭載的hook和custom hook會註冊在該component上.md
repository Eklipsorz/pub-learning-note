## 描述



### custom hook 如何在其他component使用

custom hook 使用上就跟函式一樣：
- 呼叫：只要在元件上以函式來呼叫就能使用，但會間接替各個元件註冊對應hook在元件上面，如下面的useXXX()
```
function Component() {
	useXXX();
}
```
- 呼叫引數：主要根據資訊而產生不同的hook
```
// use useXXX hook
function Component() {
	useXXX(x1, x2, ....);
}

// useXXX definition
const useXXX = (x1, x2, ....) {
	.
	.
	.
}
```
- 回傳：若要custom hook回傳的話，就直接像個函式那樣回傳，回傳型別可以是任意
```
// use useXXX hook
function Component() {
	const res = useXXX(x1, x2, ...)
}

// useXXX definition
const useCounter = (x1, x2, ...) => { 
	.
	.
	.
    return xxx
}
```
#### 若custom hook 的引數放在custom hook中的useEffect來使用

但若在custom hook中的useEffect來添加引數來處理，該引數會因為本質上不屬於是useEffect內且在useEffect的effect 會使用該引數來執行，這有可能會使它成為useEffect的deps一部分來跟著引數來重新計算。

### custom hook 在component 呼叫的話

custom hook 在component 呼叫的話，就等同在component註冊custom hook，此時custom hook和搭載其上面的hook會是：
- 若搭載其他hookA(含state)的hookB在componentA呼叫的話，其hookA和hookB也直接註冊在componentA上
- 若同個搭載其他hookA(含state)的hookB在多個component呼叫的話，每個component都會擁有各自的hookA和hookB註冊在他們身上，同個hook在多個component呼叫並不意味著他們共享著state和effect


#### 結論

多個元件使用同個hook的共享狀態會是：
- 共享hook上的業務邏輯
- 不共享state或者effect

### 案例：

```
import Card from './Card';
import useCounter from '../hooks/use-counter';

const BackwardCounter = () => {
  const counter = useCounter(false);
  return <Card>{counter}</Card>;
};

export default BackwardCounter;
```


```
import Card from './Card';
import useCounter from '../hooks/use-counter';
const ForwardCounter = () => {
  const counter = useCounter();
  return <Card>{counter}</Card>;
};

export default ForwardCounter;
```


```
import { useState, useEffect } from 'react';

const useCounter = (forwards = true) => {
  const [counter, setCounter] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      if (forwards) {
        setCounter((prevCounter) => prevCounter + 1);
      } else {
        setCounter((prevCounter) => prevCounter - 1);
      }
    }, 1000);

    return () => clearInterval(interval);
  }, [forwards]);

  return counter;
};

export default useCounter;
```


## 複習

#💻 請到/react-builder/question-review/custom-hook-project領取題目，切換至master分支，請建立一個hook來替代ForwardCounter.js和BackwardCounter.js這兩者的狀態業務邏輯 ->->-> `https://github.com/academind/react-complete-guide-code/tree/15-building-custom-react-hooks/code/03-configuring-custom-hooks/src`
<!--SR:!2022-10-23,3,250-->

---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：定義 custom hook 以及注意事項]]
References: