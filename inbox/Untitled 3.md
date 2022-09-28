## 描述


### noValidate 是對

```
return (
    <form className={styles.form} onSubmit={cartSubmitHandler} noValidate>
      <NumberInput
        label='Amount'
        attr={{
          id: `meal-item-${props.id}`,
          type: 'number',
          min: '1',
          max: '5',
          step: '1',
          defaultValue: '1',
        }}
        ref={inputRef}
      />
      <button>+ Add</button>
      {!isValidAmount && <p>Please input a amount</p>}
    </form>
  );
```

## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: