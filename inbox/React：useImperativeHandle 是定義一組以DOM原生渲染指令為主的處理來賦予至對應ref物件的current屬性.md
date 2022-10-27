## 描述

### useImperativeHandle 語法

> useImperativeHandle

> allows us to use this Component or functionalities from  inside this Component imperatively, which simple means not through the regular state props management not by controlling the component through state in the parent Component, but instead by directly calling or manipulating something in the Component programmatically


> ### 2.1 语法

> useImperativeHandle(ref, createHandle, [deps])

> 1.  `ref`  
>    需要被赋值的`ref`对象。
>2.  `createHandle`：  
>    `createHandle`函数的返回值作为`ref.current`的值。
>3.  `[deps]`  
>    依赖数组，依赖发生变化会重新执行`createHandle`函数。


重點：
- useImperativeHandle 本身是一個HOOK，會註冊在元件上
- useImperativeHandle 具體是要以指定一組以DOM原生渲染指令為主的處理來賦予至對應ref物件上的current屬性
- 語法會是：
	- ref 是被指定賦予一組以DOM原生渲染指令為主的處理之物件，具體會賦予在ref.current
	- createHandle 用來決定渲染指令的函式，會用物件來回傳一組以DOM原生渲染指令為主的處理
		- createHandle 函式所回傳正是指定ref.current所擁有的值
		- 用法：
			- xxxx可以是任意型別
		```
		useImperativeHandle(() => {
			return xxxx
		})
	   ```


	- deps 則是指定義著依賴dependency的陣列，每一次ImperativeHandle觸發時都會檢查dependency是否有任一變動，有變動才執行createHandle；沒變動不會執行
	```
	useImperativeHandle(ref, createHandle, [deps])
	```

#### 案例：

```
import React, { useImperativeHandle, useRef } from 'react';

import classes from './Button.module.css';

const Button = (props) => {
  const ref = useRef();

  useImperativeHandle(ref, () => {
    return {
      teststing: 'hi',
    };
  });
  console.log(ref)
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

export default Button;
```


![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664024431/blog/react/ImperativeHandle/simple-imperativeHandle-example_lwx992.png)

### 什麼時候執行
> ### 2.2 进阶：什么时候执行`createHandle`函数？

> 测试发现和`useLayoutEffect`执行时机一致。  
> 修改下组件`FancyInput`内容：

```
const FancyInput = React.forwardRef(function FancyInput(props, ref) {
    const inputRef = useRef();
    console.log('render 1')

    useLayoutEffect(() => {        
        console.log('useEffect1', ref)
    })

    useImperativeHandle(ref, function() {        
        debugger
        console.log('useImperativeHandle')
        return {
            focus: () => {
                inputRef.current.focus();
            }
        }
    })    

    useLayoutEffect(() => {        
        console.log('useEffect2', ref);
    })

    console.log('render 2')
    return <input ref={inputRef}  placeholder="FancyInput"/>;
})
```


![image.png](https://segmentfault.com/img/bVcVbi1 "image.png")  
> 看看控制台输出发现`createHandle`函数的执行时机和`useLayoutEffect`一致，这样就**保证了在任意位置的`useEffect`里都能拿到最新的`ref.current`的值**。

> **注意：**执行`createHandle`函数的还有个前提条件，即`useImperativeHandle`的第一个实参`ref`必须有值（否则执行`createHandle`函数也没意义啊）。

重點：
- useImperativeHandle 觸發執行的時機點和useLayoutEffect是一樣

## 複習

#🧠 React：useImperativeHandle 在元件上是什麼？ ->->-> `useImperativeHandle 本身是一個HOOK，會註冊在元件上`
<!--SR:!2022-11-04,27,250-->

#🧠 React：useImperativeHandle 用途是什麼？ ->->-> `具體是要以指定一組以DOM原生渲染指令為主的處理來賦予至對應ref物件上的current屬性`
<!--SR:!2022-10-30,3,250-->


#🧠 React：useImperativeHandle命名緣由源自於？ ->->-> `一組以DOM原生渲染指令為主的處理`


#🧠 React：useImperativeHandle 語法會是什麼？ ->->-> `useImperativeHandle(ref, createHandle, [deps])`


#🧠 React：useImperativeHandle 語法的ref是什麼？ ->->-> ` ref 是被指定賦予一組以DOM原生渲染指令為主的處理之物件`
<!--SR:!2022-11-01,25,250-->

#🧠 React：useImperativeHandle  語法的ref是被指定賦予一組以DOM原生渲染指令為主的處理之物件，那麼具體會如何被賦予？->->-> `createHandle 生成的處理來賦予在ref物件的current屬性`
<!--SR:!2022-11-05,28,250-->

#🧠 React：useImperativeHandle 語法的createHandle是什麼？ ->->-> `用來決定渲染指令的函式，會用物件來回傳一組以DOM原生渲染指令為主的處理`


#🧠 React：useImperativeHandle 語法的deps是什麼？ ->->-> `deps 則是指定義著依賴dependency的陣列，每一次ImperativeHandle觸發時都會檢查dependency是否有任一變動，有變動才執行createHandle；沒變動不會執行`
<!--SR:!2022-10-30,3,250-->


#🧠 React：useImperativeHandle 語法的觸發處理時機點？ ->->-> `與useLayoutEffect一樣`


#🧠 React：useImperativeHandle(ref, createHandle) 中的createHandler 用來決定渲染指令的函式，會用物件來回傳一組以DOM原生渲染指令為主的處理，請問它如何實現->->-> `直接在對應函式回傳任意形式的內容`

#🧠  React：useImperativeHandle(ref, createHandle) 中的createHandler 回傳的內容會是設定什麼？- ->->-> ` createHandle 函式所回傳正是指定ref.current所擁有的值`


---
Status: #🌱 
Tags:
[[React]]
Links:
[[useEffect vs. useLayoutEffect 觸發執行的時機點：前者是都會在渲染後和移除前才觸發，後者是在渲染前的layout處理時觸發韓移除前觸發]]
References:
[[@pulasiqiangZuiMoShengDehooksUseImperativeHandle]]