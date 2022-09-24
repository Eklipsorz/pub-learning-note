## 描述


在這裡會有兩個輸入欄位會使用以下元件的渲染內容，並於mount階段透過useRef來對著對應輸入欄位執行focus()來決定active element是什麼，結果會因為限制，最終會是由最後渲染的輸入欄來成為active element

```
import { useRef, useEffect } from 'react';
import classes from './Input.module.css';

const Input = (props) => {

  const inputRef = useRef()

  useEffect(() => {
    inputRef.current.focus()
  },[])

  return (
    <div
      className={`${classes.control} ${
        props.isValid === false ? classes.invalid : ''
      }`}
    >
      <label htmlFor={props.id}>{props.label}</label>
      <input
        type={props.type}
        id={props.id}
        ref={inputRef}
        value={props.value}
        onChange={props.onChange}
        onBlur={props.onBlur}
      />
    </div>
  );
};

export default Input;
```


> useImperativeHandle

> allows us to use this Component or functionalities from  inside this Component imperatively, which simple means not through the regular state props management not by controlling the component through state in the parent Component, but instead by directly calling or manipulating something in the Component programmatically


that is something you rarely wanna use and therefore, you shouldn't use it very often

  

function component

1. 大部分情況下，引數會是只有一個props

2. 少部分會有第二個引數 - ref (從外部引入進來的)

1.  function parent (props) {
2.    const ref = useRef
3.     return (
4.        <Component ref={...} />
5.      )
6.  }

8.  function Component(props, ref) {

10.   .....
11.  }

1. Component 是自製的

2. ref 是源自於parent 元件所建立的useRef回傳而來的ref

3. 當對Component標籤添加ref 這屬性(attribute)，就會在Component 對應的function component的ref引數接收到

  

  

  

useImperativeHandle(ref, callback)

  

callback：

1. 回傳一個物件，物件上會夾雜著資料

> you will be able to use from outside




## 複習


---
Status: #🌱 #📓 
Tags:
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
[[React：forwardRef 是React函式庫的方法，專門將指定元件A下的Ref物件傳送forwardRef函式，並由該函式轉發至另一個對應元件B下來對指定元件A的Ref物件進行處理]]
[[React：useImperativeHandle 是定義一組以DOM原生渲染指令為主的處理來賦予至對應ref物件的current屬性]]
References: