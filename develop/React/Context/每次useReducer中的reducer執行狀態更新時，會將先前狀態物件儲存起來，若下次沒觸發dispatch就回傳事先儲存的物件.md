

## 描述


#### 範例程式碼


```
const [testIsUpdatedReducer, testBegin] = useState(false);

const [emailState, dispatchEmail] = useReducer(emailReducer, {
	value: "",
    isValid: null,
});


const testReducer = () => {
    console.log("test reducer begin");
    testBegin((state) => !state);
};


useEffect(() => {
    console.log("emailState is changed!!!");
}, [emailState]);


return (
	<form>
		..
		..
		..
		<div className={classes.actions}>
          <Button type="submit" className={classes.btn} disabled={!formIsValid}>
            Login
          </Button>
          <div className={classes.btn} onClick={testReducer}>
            testReducer
          </div>
        </div>
	</form>
)

```

## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
Links:
References:


