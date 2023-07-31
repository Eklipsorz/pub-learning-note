## 描述


### Input 接收attributes
1. 定義Input 會有label、attr這兩大屬性(attributes)：
	- label 屬性：其屬性值用字串表示 用以呈現Input是代表什麼輸入欄的顯示元件
	- attr 屬性：定義其他元件對於Input的要求

```
import Input from '../UI/Input/Input';
import styles from './MealItemForm.module.css';

const MainItemForm = (props) => {
  return (
    <form className={styles.form}>
      <Input
        label='Amount'
        attr={{
          id: props.id,
          type: 'number',
          min: '1',
          max: '5',
          step: '1',
          defaultValue: '1',
        }}
      />
      <button>+ Add</button>
    </form>
  );
};

export default MainItemForm;
```


###  利用props所構建的特定Input
利用switch 來根據type為何來從中取特定屬性值來建立不同的Input，避免Input寫死成以number形式的Input

```
import styles from './Input.module.css';

const Input = (props) => {
  const { type, id } = props.attr;
  let NewInput = '';
  switch (type) {
    case 'number': {
      const { min, max, step, defaultValue } = props.attr;
      NewInput = (
        <input
          id={`input-${id}`}
          type={type}
          min={min}
          max={max}
          step={step}
          defaultValue={defaultValue}
        />
      );
      break;
    }
    default: {
      NewInput = <input type={type} id={`input-${id}`} />;
      break;
    }
  }

  return (
    <div className={styles.input}>
      <label htmlFor={`input-${id}`}>{props.label}</label>
      {NewInput}
    </div>
  );
};

export default Input;
```



## 複習


---
Status: #🌱 #📓 
Tags:
[[food-order-project]]
Links:

References: