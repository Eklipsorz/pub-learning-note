## 描述


### 若console在useReducer之後

若console在useReducer之後，其console.log會在印出八次hi reducer，才印出hi login component
```
const reducer = (prevState, action) => {
  console.log('hi reducer');
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { value: action.value, isValid: action.value.includes('@') };
    case 'INPUT_BLUR':
      return { value: prevState.value, isValid: prevState.isValid };
    default:
      return { value: '', isValid: null };
  }
};

const Login = (props) => {
  const [emailState, emailDispatch] = useReducer(reducer, {
    value: '',
    isValid: null,
  });
  console.log('hi login component');
  /*
  
	  do something
	  
  */
  const emailChangeHandler = (event) => {
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '2' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '3' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    setFormIsValid(
      .........
    );
  };

	
}
```



![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663439693/blog/react/state/useReducer/after-useReducer-result_p0u5y1.png)

### 若console在useReducer之前

若console在useReducer之後，其console.log會在印出八次hi reducer之前印出hi login component
```
const reducer = (prevState, action) => {
  console.log('hi reducer');
  switch (action.type) {
    case 'INPUT_CHANGE':
      return { value: action.value, isValid: action.value.includes('@') };
    case 'INPUT_BLUR':
      return { value: prevState.value, isValid: prevState.isValid };
    default:
      return { value: '', isValid: null };
  }
};

const Login = (props) => {
  console.log('hi login component');
  const [emailState, emailDispatch] = useReducer(reducer, {
    value: '',
    isValid: null,
  });
  
  /*
  
	  do something
	  
  */
  const emailChangeHandler = (event) => {
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '2' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: '3' });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    emailDispatch({ type: 'INPUT_CHANGE', value: event.target.value });
    setFormIsValid(
      .........
    );
  };

	
}
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1663439884/blog/react/state/useReducer/before-useReducer-result_syj60t.png)
## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: