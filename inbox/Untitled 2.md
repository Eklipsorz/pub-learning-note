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


## 複習


---
Status: #🌱 #📓 
Tags:
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
References: