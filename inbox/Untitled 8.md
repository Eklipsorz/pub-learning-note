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

## 複習


---
Status: #🌱 
Tags:
Links:
References: