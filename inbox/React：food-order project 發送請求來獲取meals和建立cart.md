## 描述


### 使用useHttp 來發送獲取meals的請求
```
  const [meals, setMeals] = useState([]);
  const { error, isLoading, sendRequest: fetchData } = useHttp();
  
  useEffect(() => {
    console.log('hii this effect')
    const options = {
      url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/meals.json',
    };

    const handler = (data) => {
      const transformedMeals = [];

      for (let key in data) {
        transformedMeals.push({
          id: key,
          name: data[key].name,
          intro: data[key].intro,
          price: data[key].price,
        });
      }
      setMeals(transformedMeals);
    };

    fetchData(options, handler);
  }, [fetchData]);
```

#### 根據回應來渲染

```
if (isLoading) {
    return (
      <section className={styles.MealsLoading}>
        <p>Loading...</p>
      </section>
    );
  }

  if (error) {
    return (
      <section className={styles.MealsError}>
        <p>{error}</p>
      </section>
    );
  }

  console.log('top level')

  return (
    <div className={styles['meals-list']}>
      {console.log('render')}
      {meals.map((meal) => (
        <MealItem
          id={meal.id}
          key={meal.id}
          name={meal.name}
          intro={meal.intro}
          price={meal.price}
        ></MealItem>
      ))}
    </div>
  );
```

### 使用useHttp 來建立購物車的請求



在cart.js元件下指定發送POST請求來建立cart，並於checkout元件安置confirmHandler事件處理器
```
  const confirmHandler = (userData) => {
    const options = {
      url: 'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/orders.json',
      method: 'POST',
      headers: { 'content-type': 'application/json' },
      body: JSON.stringify({
        user: userData,
        orderedItems: cartCtx.items,
      }),
    };

    createCartData(options);
  };


  return (
    <Modal onClick={props.onHideCart}>
      <div className={styles['cart-items']}>
        {cartCtx.items.map((item) => (
          <CartItem
            id={item.id}
            key={item.id}
            name={item.name}
            price={item.price}
            amount={item.amount}
            onAdd={addToItemHandler.bind(null, item)}
            onRemove={removeItemHandler.bind(null, item.id)}
          />
        ))}
      </div>

      <div className={styles['total']}>
        <h3>Total Amount</h3>
        <h3>${totalAmount}</h3>
      </div>
      {checkoutIsShown && (
        <Checkout onClose={props.onHideCart} onConfirom={confirmHandler} />
      )}
      {!checkoutIsShown && cartAction}
    </Modal>
  );
```

checkout 表單的提交事件會調用props.onConfirm來建立購物車
```
  const confirmHandler = (event) => {
    event.preventDefault();
    event.stopPropagation();

    if (!formIsValid) return;
    console.log(
      'submit',
      enteredName,
      enteredStreet,
      enteredPostalCode,
      enteredCity,
    );

    props.onConfirom({
      name: enteredName,
      postalCode: enteredPostalCode,
      street: enteredStreet,
      city: enteredCity,
    });
    
    enteredNameReset();
    enteredStreetReset();
    enteredPostalCodeReset();
    enteredCityReset();
  };
```


---
Status: #🌱 
Tags:
[[React]]
Links:
References: