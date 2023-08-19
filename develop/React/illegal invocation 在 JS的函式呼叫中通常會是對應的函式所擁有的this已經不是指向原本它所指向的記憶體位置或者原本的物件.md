



## 描述


### 問題描述

#### 設定focus 為 inputRef.current.focus 出現錯誤
若貿然使用以下

```
  const inputRef = useRef();

  const activate = () => {
    inputRef.current.focus();
  };

  useImperativeHandle(ref, () => {
    return {
      focus: inputRef.current.focus,
    };
  });
```

會顯示以下錯誤訊息
```
Login.js:106 Uncaught TypeError: Illegal invocation
    at submitHandler (Login.js:106:1)
    at HTMLUnknownElement.callCallback (react-dom.development.js:4164:1)
    at Object.invokeGuardedCallbackDev (react-dom.development.js:4213:1)
    at invokeGuardedCallback (react-dom.development.js:4277:1)
    at invokeGuardedCallbackAndCatchFirstError (react-dom.development.js:4291:1)
    at executeDispatch (react-dom.development.js:9041:1)
    at processDispatchQueueItemsInOrder (react-dom.development.js:9073:1)
    at processDispatchQueue (react-dom.development.js:9086:1)
    at dispatchEventsForPlugins (react-dom.development.js:9097:1)
    at react-dom.development.js:9288:1
    at batchedUpdates$1 (react-dom.development.js:26140:1)
    at batchedUpdates (react-dom.development.js:3991:1)
    at dispatchEventForPluginEventSystem (react-dom.development.js:9287:1)
    at dispatchEventWithEnableCapturePhaseSelectiveHydrationWithoutDiscreteEventReplay (react-dom.development.js:6465:1)
    at dispatchEvent (react-dom.development.js:6457:1)
    at dispatchDiscreteEvent (react-dom.development.js:6430:1)
```

重點：
- 由於inputRef.current.focus 的 this 是指向inputRef.current對應的記憶體區塊，但因為被當成函式物件來傳遞其記憶體位址給予focus方法，所以就使focus的method失去原有的this - inputRef.current對應的記憶體區塊


#### 設定focus 為activate 會正常執行
```
  const inputRef = useRef();

  const activate = () => {
    inputRef.current.focus();
  };

  useImperativeHandle(ref, () => {
    return {
      focus: activate,
    };
  });
```

重點：
- focus的method失去原有的this - inputRef.current對應的記憶體區塊 解法概念：讓focus的this以inputRef.current對應的記憶體區塊為主
- 具體做法之一：
	- 新增一個新的函式呼叫，並在內部定義 函式的closure來將inputRef.current對應至目前元件所對應的記憶體位址 + implicit this bind 來呼叫其focus
### 主因




[[@IllegalInvocationErrors]]

>  "Illegal invocation" errors in JavaScript
> The error is thrown when calling a function whose `this` keyword isn't referring to the object where it originally did, i.e. when the "context" of the function is lost.


重點：
- 若執行函式呼叫時，代表對應的函式所擁有的this已經不是指向原本它所指向的記憶體位置或者原本的物件
- 延續第一點，若堅持執行會發生預期外的錯誤

## 複習
#🧠 illegal invocation 在 JS的函式呼叫中通常會是什麼問題？ ->->-> `若執行函式呼叫時，代表對應的函式所擁有的this已經不是指向原本它所指向的記憶體位置或者原本的物件`
<!--SR:!2023-06-27,74,250-->

#🧠 illegal invocation 在 JS的函式呼叫中通常會是若執行函式呼叫時，代表對應的函式所擁有的this已經不是指向原本它所指向的記憶體位置或者原本的物件，那麼貿然執行會是如何？ ->->-> `若堅持執行會發生預期外的錯誤`
<!--SR:!2024-01-05,186,250-->

#🧠 請問以下程式碼為何會出現illegal invocation？ 以下的程式碼是由元件1定義元件2所賦予的ref物件之過程，並且在元件2呼叫該focus  ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677862783/blog/javascript/this-binding/illegal-invocation-function/illegal-invocation-function-problem_u3slap.png)->->-> `由於inputRef.current.focus 的 this 是指向inputRef.current對應的記憶體區塊，但因為被當成函式物件來傳遞其記憶體位址給予focus方法，所以就使focus的method失去原有的this - inputRef.current對應的記憶體區塊`
<!--SR:!2023-06-11,38,230-->

#🧠 請說明為何以下寫法可以解決focus: inputRef.current.focus所造成的illegal invocation 問題？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677862782/blog/javascript/this-binding/illegal-invocation-function/illegal-invocation-function-solution_ibtac4.png) ->->-> `由於利用function的closure將focus的this鎖定在inputRef.current，這樣以後給其他元件呼叫時，就固定以該this來執行`
<!--SR:!2024-04-27,251,250-->


#🧠 請問以下程式碼為何會出現illegal invocation？其原因為由於inputRef.current.focus 的 this 是指向inputRef.current對應的記憶體區塊，但因為被當成函式物件來傳遞其記憶體位址給予focus方法，所以就使focus的method失去原有的this - inputRef.current對應的記憶體區塊，所以解法概念為何？具體為何？ ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1677862783/blog/javascript/this-binding/illegal-invocation-function/illegal-invocation-function-problem_u3slap.png)->->-> `- focus的method失去原有的this - inputRef.current對應的記憶體區塊 解法概念：讓focus的this以inputRef.current對應的記憶體區塊為主。具體做法之一： - 新增一個新的函式呼叫，並在內部定義 函式的closure來將inputRef.current對應至目前元件所對應的記憶體位址 + implicit this bind 來呼叫其focus`
<!--SR:!2023-05-06,38,250-->



---
Status: #🌱 
Tags:
[[JavaScript]] - [[React]]
Links:
References:
[[@IllegalInvocationErrors]]