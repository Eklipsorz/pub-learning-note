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
const useXXX = (x1, x2, ....) => {
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


#🧠 React：custom hook 使用上就跟函式一樣，請說明hook的使用方式？ ->->-> `如同函式呼叫那樣來調用hook，比如function Component() { useXXX(); }`
<!--SR:!2023-11-03,228,248-->

#🧠 React：custom hook 在component呼叫的話，在記憶體上等同於什麼？  ->->-> `在component註冊custom hook以及其資訊`
<!--SR:!2024-05-21,260,228-->

#🧠 React：custom hook 在component呼叫的話，就等同在component註冊custom hook，若custom hookA 搭載其他hookB，請問對於在元件呼叫來說是什麼意思？->->-> `hookB和hookA會一同註冊在同個component`
<!--SR:!2024-12-23,492,250-->


#🧠 React：custom hook 在component呼叫的話，就等同在component註冊custom hook，那麼多個component 呼叫著同個custom hook，那麼會有什麼共享情況？ ->->-> `這些component共享著同個custom hook的業務邏輯，但不共享state或者effect。`
<!--SR:!2023-08-29,196,250-->

#🧠 React：custom hook 在component呼叫的話，就等同在component註冊custom hook，那麼多個component 呼叫著同個custom hook，那麼不共享state或者effect會是因爲著？  ->->-> `首先每個component呼叫hook，就等同於將相關資訊註冊在對應component，換言之，就是每個component的hook都是獨立的`
<!--SR:!2023-09-06,198,248-->

#🧠 React：custom hook 在component呼叫的話，就等同在component註冊custom hook，那麼多個component 呼叫著同個custom hook，那麼會是指多個component 共享同個state或者effect嗎？->->-> `並不是`
<!--SR:!2023-10-03,212,248-->

#🧠 React：custom hook 使用上就跟函式一樣，請說明hook在使用上會添加什麼形式來使用？形式會是如何？分別講出hook定義和實際使用的形式->->-> `主要以函式來夾雜指定參數來呼叫使用，hook定義會是const useXXX = (x1, x2, ....) => {}，函式呼叫會是useXXX(x1, x2, ....);`
<!--SR:!2023-08-29,182,230-->


#🧠  React：custom hook 使用上就跟函式一樣，那麼會像函式那樣回傳東西嗎？形式會是如何？分別講出hook定義和實際使用的形式->->-> `會，hook定義會是是const useXXX = (x1, x2, ....) => { return xxxx }。函式呼叫的話會是const res = useXXX(x1, x2, ...) `
<!--SR:!2023-10-12,216,248-->

#🧠 React：若custom hook 的引數放在custom hook中的useEffect來使用，需要添加其為deps嗎？ 為什麼->->-> `視情況需要，本質上custom hook若被componentA使用，肯定會夥同內部的useEffect一同註冊componentA，換言之，皆為在元件內部，若引數本質上是代表著元件互動，那麼勢必很有可能得放在deps來滿足其目標。`
<!--SR:!2023-11-19,127,208-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：定義 custom hook 以及注意事項]]
References: