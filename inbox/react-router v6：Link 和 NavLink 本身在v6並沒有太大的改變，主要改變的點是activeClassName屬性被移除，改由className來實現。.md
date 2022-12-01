## 描述





### v5 vs. v6： Link 和 NavLink

Link 和 NavLink 本身在v6並沒有太大的改變，主要改變的點：
- v6 ：NavLink上的activeClassName屬性被移除，改由className來實現


#### NavLink 的 className

若NavLink的 className是一個函式物件，react-router會進行特殊處理，具體提供navigation 狀態物件來當作函式的參數來處理並回傳對應的class 名稱，形式會是：
	- 函式物件是一個參數的函式，其參數會由react-router所提供的navigation 狀態物件
	- navigation 狀態物件的屬性(property) isActive為布林值：
		- 當目前NavLink為active element，isActive為ture；否則為false

```
function (navData) {
	return .....
}
```


##### 範例

```
const MainHeader = () => {
  return (
    <header className={classes.header}>
      <nav>
        <ul>
          <li>
            <NavLink
              className={(navData) => (navData.isActive ? classes.active : '')}
              to='/welcome'
            >
              Welcome
            </NavLink>
          </li>
          <li>
            <NavLink
              className={(navData) => (navData.isActive ? classes.active : '')}
              to='/products'
            >
              Products
            </NavLink>
          </li>
        </ul>
      </nav>
    </header>
  );
};
```


### v5 vs. v6：useParams 
useParams 用法沒變動

## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
[[react-router v6：從多個路徑挑選一個路徑和Route 語法之間的改變]]
References: