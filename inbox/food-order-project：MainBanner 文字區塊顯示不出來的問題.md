## 描述


### MainBanner 結構以及所在

```
import React from 'react';
import MainBanner from './MainBanner';

import styles from './MainHeader.module.css';

const MainHeader = (props) => {
  return (
    <React.Fragment>
      <MainBanner />
      <div className={styles.header}>
        <h2>ReactMeals</h2>
        <button>Your Cart</button>
      </div>
    </React.Fragment>
  );
};

export default MainHeader;
```


### MainBanner 文字區塊顯示不出來的問題

起因為：
- main-banner 高寬已經被設定了，所以裡頭存放的圖片和文字很有可能因為其中一方太大而被排擠到看不到的地方，但仍屬於main-banner區塊裡頭
- 在這裡是因為圖片太大，造成文字部分往下放到看不到的地方

```
import styles from './MainBanner.module.css';

const MainBanner = (props) => {
  return (
    <div className={styles['main-banner']}>
      <img alt='meals' src='./meals.jpg' />
      <div>
        <h2>Delicious Food, Delivered To You</h2>
        <p>
          Choose your favorite meal from our broad selection of available meals
          and enjoy a delicious lunch or dinner at home.
        </p>
        <p>
          All our meals are cooked with high-quality ingredients, just-in-time
          and of course by experienced chefs!
        </p>
      </div>
    </div>
  );
};

export default MainBanner;

```


```
.main-banner {
  /* positioning */
  z-index: 0;
  /* display */
  /* box model */
  width: 100%;
  height: 25rem;
  overflow: hidden;
  /* font or others */
}

.main-banner img {
  width: 110%;
  height: 100%;
  object-fit: cover;
  transform: rotateZ(-5deg) translateY(-4rem) translateX(-1rem);
}
```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664204746/blog/react/food-order/problem1_v3wmel.png)
### 解法

1. 將文字區塊採用summary class
2. summary class會試著往上挪移


```
.main-banner {
  /* positioning */
  z-index: 0;
  /* display */
  /* box model */
  width: 100%;
  height: 25rem;
  overflow: hidden;
  /* font or others */
}

.main-banner img {
  width: 110%;
  height: 100%;
  object-fit: cover;
  transform: rotateZ(-5deg) translateY(-4rem) translateX(-1rem);
}

.summary {
  /* positioning */
  position: relative;
  top: -10rem;
  /* display */
  /* box model */

  /* font or others */
}

```

![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1664204974/blog/react/food-order/problem1-solution_gmimjr.png)
## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: