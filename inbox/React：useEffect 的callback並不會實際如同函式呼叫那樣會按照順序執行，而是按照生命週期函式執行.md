## 描述



### 實驗
在這裏分別在functional component 中的useEffect 、top level code、渲染部分做出console.log

useEffect  部分為：
```
console.log('hii this effect')
```

top level code 是指functional component上還未進入任何hook或者render部分的code，其console會是：
```
  console.log('top level')
```

渲染部分則是指functional component回傳的渲染部分添加\{\}來執行JS
```
return (
	 {console.log('render')}
)
```



```
import { useEffect, useState } from 'react';
import useHttp from '../../hooks/use-http';
import MealItem from './MealItem';
import styles from './Meals.module.css';

const Meals = (props) => {
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
};

export default Meals;
```

#### 實驗結果：

從結果得知，一開始會執行top level而先印出top level，接著useEffect的確呼叫到了，但裡頭callback、deps是直接按照生命週期函式而執行，在這時還未執行render，所以等到render結束後才執行callback。前面三段可以證實

```
top level
render
hii this effect
top level
render
```

後面兩段是因為effect本身觸發setState而進入渲染，此時又會執行到top level 和render，而useEffect也被呼叫到，只是裡頭callback本身設定成\[\]，所以並不會在updating 和unmounting階段執行

## 複習

#🧠 React：useEffect 本身在functional component是按照生命週期函式執行？還是如何？ ->->-> `本身會按照函式呼叫那樣按照順序，執行到呼叫就執行呼叫`
<!--SR:!2022-10-31,2,230-->

#🧠 React：useEffect 本身和useEffect(callback, \[deps\])中的callback、deps之間差異為何？ ->->-> `useEffect本身在functional component會是個函式呼叫，執行到就呼叫，而callback、deps則是按照元件的生命週期函式來執行。`
<!--SR:!2022-11-08,10,250-->

#🧠 React：在這裏分別在functional component 中的useEffect 、top level code、渲染部分做出console.log，其結果會是如下，請問useEffect有被執行到嗎？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666681597/blog/react/effect/useEffect/useEffect-result_b7qfub.png)->->-> `其本身有呼叫到`
<!--SR:!2022-11-06,8,250-->

#🧠 React：在這裏分別在functional component 中的useEffect 、top level code、渲染部分做出console.log，其結果會是如下，請問為何useEffect中的callback的執行順序為何是在render之後？![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666681597/blog/react/effect/useEffect/useEffect-result_b7qfub.png)->->-> `由於callback本身是按照生命週期函式來執行，也就是componentDidMount、componentDidUpdate、componentWillUnmount時執行，在那時會是在render之後才執行，故此在render之後執行`
<!--SR:!2022-10-29,3,250-->

#🧠 React：在這裏分別在functional component 中的useEffect 、top level code、渲染部分做出console.log，其結果會是如下，請說明執行狀況![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1666681597/blog/react/effect/useEffect/useEffect-result_b7qfub.png) ->->-> `從結果得知，一開始會執行top level而先印出top level，接著useEffect的確呼叫到了，但裡頭callback、deps是直接按照生命週期函式而執行，在這時還未執行render，所以等到render結束後才執行callback。前面三段可以證實`
<!--SR:!2022-11-08,10,250-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: