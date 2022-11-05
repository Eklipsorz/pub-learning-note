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

#💻 請至/react-builder/question-review/form-adv-practice 領取題目並切換至useInput-with-useReducer分支， 請在/src/hooks/use-input.js中改使用useReducer來實現該hook function原有的業務邏輯。->->-> `https://github.com/academind/react-complete-guide-code/blob/16-working-with-forms/code/12-finished/src/hooks/use-input.js`
<!--SR:!2022-12-03,28,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
[[React：使用custom hook來重構表格案例-基本表格]]
[[React：使用custom hook來重構表格]]
References: