## 描述


> \<NavLink\>

> A special version of the \<Link\> that will add styling attributes to the rendered element when it matches the current URL.

we often want to highlight the active link in the navigation

-> NavLink 本質上是以Link元件，只是會用特定樣式來顯示目前頁面是屬於哪個Link

> ## [activeClassName: string](https://v5.reactrouter.com/web/api/NavLink/activeclassname-string)

> The class to give the element when it is active. The default given class is `active`. This will be joined with the `className` prop.

重點：
- NavLink 在react-router中是一個component，主要是以Link元件為基礎來提示目前頁面是屬於哪個Link component
- 本質是Link 元件，只是多了一些樣式來渲染
- 常見用法為
	- to：指定要導向哪個頁面，具體會以瀏覽器的absolute URL和 relative URL規範所定義的root path為主
	- activeClassName：則是指定當Link 元件為active element時就將對應DOM節點的class設定class-name
	- xxxx1 則是被綁定頁面連結的hypertext
```
<NavLink to="xxx" activeClassName="class-name"> xxxx1 </NavLink>
```
- 載入方式：由react-router-dom所提供
```
import { NavLink } from 'react-router-dom';
```



### 案例
```
import { NavLink } from 'react-router-dom';
import styles from './MainHeader.module.css';
const MainHeader = () => {
  return (
    <header className={styles.header}>
      <nav>
        <ul>
          <li>
            <NavLink to='/welcome' activeClassName={styles.active}>
              Welcome
            </NavLink>
          </li>
          <li>
            <NavLink to='/products' activeClassName={styles.active}>
              Products
            </NavLink>
          </li>
        </ul>
      </nav>
    </header>
  );
};

export default MainHeader;
```

## 複習


---
Status: #🌱 #📝 
Tags:
[[React]]
Links:
[[relative URL 會是以特定資源A的所在目錄位置為參考點來找到特定資源B的路徑，特定路徑A通常會是以特定資源A的所在目錄位置為參考點來指定]]
[[absolute URL：意指為特定資源在網路上的完整位置，其完整位置包含了該資源在網路上的完整位置、該資源在特定協定網路下的完整位置、該資源在特定協定網路之特定主機下的完整位置]]
References: