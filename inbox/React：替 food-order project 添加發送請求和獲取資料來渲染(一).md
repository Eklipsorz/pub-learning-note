## 描述


```
 const fetchData = useCallback(async () => {
    const response = await fetch(
      'https://react-test-http-d24a5-default-rtdb.asia-southeast1.firebasedatabase.app/meals.json',
    );

    const data = await response.json();
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
  }, []);

  useEffect(() => {
    fetchData();
  }, [fetchData]);
```

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: