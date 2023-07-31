## 描述


```
import { useReducer } from 'react';

const initialState = {
  value: '',
  isTouched: false,
};

const formReducer = (prevState, action) => {
  let newState = null;

  switch (action.type) {
    case 'INPUT':
      newState = { value: action.value, isTouched: prevState.isTouched };
      break;
    case 'BLUR':
      newState = { value: prevState.value, isTouched: true };
      break;
    case 'RESET':
      newState = { value: '', isTouched: false };
      break;
    default:
      newState = { value: '', isTouched: false };
      break;
  }

  return newState;
};

const useInput = (validation) => {
  const [formState, dispatch] = useReducer(formReducer, initialState);

  const valueIsValid = validation(formState.value);
  const hasError = !valueIsValid && formState.isTouched;

  const valueChangeHandler = (event) => {
    dispatch({ type: 'INPUT', value: event.target.value });
  };

  const inputBlurHandler = (event) => {
    dispatch({ type: 'BLUR' });
  };

  const reset = () => {
    dispatch({ type: 'RESET' });
  };

  return {
    value: formState.value,
    hasError,
    valueIsValid,
    valueChangeHandler,
    inputBlurHandler,
    reset,
  };
};

export default useInput;

```

## 複習



---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用custom hook來重構表格案例-基本表格]]
[[React：使用custom hook來重構表格]]
References: