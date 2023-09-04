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


	- deps 則是指定義著依賴dependency的陣列，每一次ImperativeHandle觸發時都會檢查dependency是否有任一變動，有變動才執行createHandle；沒變動不會執行createHandle
	```
	useImperativeHandle(ref, createHandle, [deps])
	```

### useImperativeHandle的deps目的
useImperativeHandle的deps目的是用來做優化處理，減少createHandle執行並且直接回傳相同結果，所以會儲存什麼作為比對和回傳結果

### 執行模式

首次在mounting階段時，會因為沒有事先存下的deps資訊而先執行createHandle，接著將對應deps資訊和handle儲存起來好比對和回傳

在updating階段時，每一次執行到都會比對目前deps內容是否與上一次render最近儲存到的deps一樣，若不一樣的話，就執行createHandle，接著將對應的deps資訊和handle儲存起來好比對和回傳；若一樣的話，就回傳最近的handle給ref物件之current屬性

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

#### 案例：

在Login元件上安置一個狀態count，並放到Input元件當作其useImperativeHandle的deps，其deps會是如下，並且分配activate函式給對應Login元件上的ref物件之current屬性
```
[Boolean(props.testVal)]
```

而testVal會隨著提交按鈕次數而增加，經過三次提交按鈕的結果會是

```
---------- mounting
allocation 0
---------- 第一次提交按鈕
activate 0
allocation 1
---------- 第二次提交按鈕
activate 1
---------- 第三次提交按鈕
activate 1
```


在這裡由於mounting並沒有任何事先儲存的內容，所以useImperativeHandle並不會比對，接著執行createHandleFn來分配並得到以下結果，除此之外，還得到對應handle和deps，這些內容會由React來儲存
```
allocation 0
```

接著第一次提交按鈕點擊時，由於會因此會呼叫activation，接著因為setCount而觸發Login渲染以及將count設定為1，接著再次執行Input，因而使得useImperativeHandle執行，在這裡由於是updating，所以會比對目前deps內容和上一個render儲存到的deps內容進行比對，發現為不一樣，執行useImperativeHandle，得到對應handle和deps，接著React來儲存， 其執行結果會如同下面allocation的部分
```
activate 0
allocation 1
```

隨後第二次和第三次的提交按鈕點擊時，都因為會使得useImperativeHandle比對內容時都皆為一樣，而不執行createImperativeHandle，但會回傳曾經產生的handle給對應ref物件之current屬性


Login.js 
```
  const [count, setCount] = useState(0);

  const submitHandler = (event) => {
    event.preventDefault();
    console.log('submit', emailState, passwordState);

    if (emailIsValid && passwordIsValid) {
      authCtx.onLogin(emailState.value, passwordState.value);
    } else if (!emailIsValid) {
      emailInputRef.current.focus();
    } else {
      passwordInputRef.current.focus();
    }
    setCount((count) => count + 1);
  };

   return (
    <Card className={classes.login}>
      <form onSubmit={submitHandler}>
        {/* <div
          className={`${classes.control} ${
            emailState.isValid === false ? classes.invalid : ''
          }`}
        >
          <label htmlFor='email'>E-Mail</label>
          <input
            type='email'
            id='email'
            value={emailState.value}
            onChange={emailChangeHandler}
            onBlur={validateEmailHandler}
          />
        </div> */}
        <Input
          type='email'
          id='email'
          label='E-Mail'
          isValid={emailIsValid}
          value={emailState.value}
          ref={emailInputRef}
          testVal={count}
          onChange={emailChangeHandler}
          onBlur={validateEmailHandler}
        />
        .
        .
  )
```

Input.js
```
  const activate = () => {
	console.log('activate', props.testVal);
  };

  useImperativeHandle(
    ref,
    () => {
	  console.log('allocation', props.testVal);
      return {
        focus: activate,
      };
    },
    [Boolean(props.testVal)],
  );
```



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
<!--SR:!2024-11-03,473,250-->

#🧠 React：useImperativeHandle 用途是什麼？ ->->-> `具體是要以指定一組以DOM原生渲染指令為主的處理來賦予至對應ref物件上的current屬性`
<!--SR:!2024-01-12,178,230-->


#🧠 React：useImperativeHandle命名緣由源自於？ ->->-> `一組以DOM原生渲染指令為主的處理`
<!--SR:!2024-05-09,290,230-->


#🧠 React：useImperativeHandle 語法會是什麼？ ->->-> `useImperativeHandle(ref, createHandle, [deps])`
<!--SR:!2024-01-10,266,250-->


#🧠 React：useImperativeHandle 語法的ref是什麼？ ->->-> ` ref 是被指定賦予一組以DOM原生渲染指令為主的處理之物件`
<!--SR:!2024-10-13,453,250-->

#🧠 React：useImperativeHandle  語法的ref是被指定賦予一組以DOM原生渲染指令為主的處理之物件，那麼具體會如何被賦予？->->-> `createHandle 生成的處理來賦予在ref物件的current屬性`
<!--SR:!2024-12-16,504,250-->

#🧠 React：useImperativeHandle 語法的createHandle是什麼？ ->->-> `用來決定渲染指令的函式，會用物件來回傳一組以DOM原生渲染指令為主的處理`
<!--SR:!2023-12-03,90,230-->


#🧠 React：useImperativeHandle 語法的deps是什麼？ ->->-> `deps 則是指定義著依賴dependency的陣列，每一次ImperativeHandle觸發時都會檢查dependency是否有任一變動，有變動才執行createHandle；沒變動不會執行createHandle`
<!--SR:!2023-09-22,188,230-->


#🧠 React：useImperativeHandle 語法的觸發處理時機點？ ->->-> `與useLayoutEffect一樣`
<!--SR:!2023-09-05,196,250-->


#🧠 React：useImperativeHandle(ref, createHandle) 中的createHandler 用來決定渲染指令的函式，會用物件來回傳一組以DOM原生渲染指令為主的處理，請問它如何實現->->-> `直接在對應函式回傳任意形式的內容`
<!--SR:!2023-12-09,100,230-->

#🧠  React：useImperativeHandle(ref, createHandle) 中的createHandler 回傳的內容會是設定什麼？- ->->-> ` createHandle 函式所回傳正是指定ref.current所擁有的值`
<!--SR:!2023-09-03,195,250-->

#🧠 React：useImperativeHandle在mounting 階段和updating階段會是什麼？ ->->-> `首次在mounting階段時，會因為沒有事先存下的deps資訊而先執行createHandle，接著將對應deps資訊和handle儲存起來好比對和回傳。 在updating階段時，每一次執行到都會比對目前deps內容是否與上一次render最近儲存到的deps一樣，若不一樣的話，就執行createHandle，接著將對應的deps資訊和handle儲存起來好比對和回傳；若一樣的話，就回傳最近的handle給ref物件之current屬性`
<!--SR:!2023-12-10,159,229-->

#🧠 React：useImperativeHandle在mounting 階段會是什麼？->->-> `首次在mounting階段時，會因為沒有事先存下的deps資訊而先執行createHandle，接著將對應deps資訊和handle儲存起來好比對和回傳
<!--SR:!2023-12-14,242,249-->

#🧠 React：useImperativeHandle在updating 階段會是什麼？ ->->-> `在updating階段時，每一次執行到都會比對目前deps內容是否與上一次render最近儲存到的deps一樣，若不一樣的話，就執行createHandle，接著將對應的deps資訊和handle儲存起來好比對和回傳；若一樣的話，就回傳最近的handle給ref物件之current屬性`
<!--SR:!2024-03-09,299,249-->

#🧠 React：useImperativeHandle的deps目的是用來做什麼？ ->->-> `用來做優化處理，減少createHandle執行並且直接回傳相同結果。`
<!--SR:!2023-11-26,232,249-->
`

#🧠  React：useImperativeHandle的deps目的是用來做優化處理，減少createHandle執行並且直接回傳相同結果，所以會儲存什麼作為比對和回傳結果 ->->-> `deps資訊和handle`
<!--SR:!2024-03-20,299,249-->



---
Status: #🌱 
Tags:
[[React]]
Links:
[[useEffect vs. useLayoutEffect 觸發執行的時機點：前者是都會在渲染後和移除前才觸發，後者是在渲染前的layout處理時觸發韓移除前觸發]]
References:
[[@pulasiqiangZuiMoShengDehooksUseImperativeHandle]]