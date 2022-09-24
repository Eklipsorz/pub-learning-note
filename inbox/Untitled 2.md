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


### forwarding 命名緣由
> to send a letter, etc., especially from someone's old address to their new address, or to send a letter, email, etc. that you have received to someone else

重點：
- forward：將從特定事物A獲取的事物發送給其他事物B


## 複習


---
Status: #🌱 #📓 
Tags:
Links:
[[DOM.focus() 會指在同一份文件下，將特定元件標記為active element。一份文件裡只會有0~1個active element]]
References: