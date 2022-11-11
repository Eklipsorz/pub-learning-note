## 描述

### 插入Layout元件，並用路由器根據URL變動而選出的瀏覽畫面來當作後裔節點來插入

```
import Layout from './components/layout/Layout';

function App() {
  return (
    <Layout>
      <Switch>
        <Route path='/' exact>
          <Redirect to='/quotes' />
        </Route>
        <Route path='/quotes' exact>
          <Quotes />
        </Route>
        <Route path='/quotes/:quoteId'>
          <Quote />
        </Route>
        <Route path='/new-quote'>
          <NewQuote />
        </Route>
      </Switch>
    </Layout>
  );
}
```




### 打造Layout元件並安放MainNavigation以及可用props插入資料的地方

```
import React from 'react';
import MainNavigation from './MainNavigation';
import styles from './Layout.module.css';

const Layout = (props) => {
  return (
    <React.Fragment>
      <MainNavigation />
      <main className={styles['main']}>{props.children}</main>
    </React.Fragment>
  );
};

export default Layout;
```



### 建立 MainNavigation 元件
```
import { NavLink } from 'react-router-dom';
import styles from './MainNavigation.module.css';

const MainNavigation = () => {
  return (
    <header className={styles['header']}>
      <div className={styles['logo']}>Greate Quotes</div>
      <nav className={styles['nav']}>
        <ul>
          <li>
            <NavLink to='/quotes' activeClassName={styles['active']}>
              All Quotes
            </NavLink>
          </li>
          <li>
            <NavLink to='/new-quote' activeClassName={styles['active']}>
              Add a Quote
            </NavLink>
          </li>
        </ul>
      </nav>
    </header>
  );
};

export default MainNavigation;
```


## 複習

#💻 Question :: ->->-> ``


---
Status: #🌱 
Tags:
[[React]]
Links:
[[main 元素最主要是存放網頁主要內容的區塊]]
[[header 是一個網頁元素，主要會以網頁畫面上的頂部區塊呈現引導使用者進入應用程式的區塊]]
[[React：layout component 會是以元件來表示一個多個固定元件的固定擺放配置，並允許接收props資訊來從其他元件中接收資訊並來構成適合該元件使用的元件]]
[[navigation 是網頁用來幫助使用者導向其他頁面的區塊，具體區塊內會含有多個hyperlink給予使用者做互動來導向]]
References: