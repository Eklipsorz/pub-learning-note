## 描述



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