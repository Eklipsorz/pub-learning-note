## 描述


>condition content
> 1. it's about rendering different output under different conditions

重點：
- condition content 是根據執行情況來調整渲染內容的技術
-   具體有幾種形式：
	1. 使用 條件式 ? 滿足條件式會有的渲染內容 :  不滿足下會有的渲染內容 來構成
	2. 使用 兩個條件式 && 滿足條件式會有的渲染內容  來構成
	3. 從渲染層面移除條件判斷，在元件的業務邏輯下設定條件來指定要輸出的內容，並於渲染層級以輸出結果來渲染



### 使用 條件式 ? 滿足條件式會有的渲染內容 :  不滿足下會有的渲染內容 來構成

在這裡使用
```
{matchedItems.length === 0 ? (
          <p>No expenses found.</p>
        ) : (
          matchedItems.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))
)}
```

來加入以下內容：
```
import ExpenseItem from './ExpenseItem';
import ExpensesFilter from './ExpensesFilter';
import Card from '../UI/Card';
import { useState } from 'react';
import './Expenses.css';

function Expenses(props) {
  const { items } = props;
  const [filteredYear, setFilteredYear] = useState('2020');

  const filterChangeHandler = (filteredYear) => {
    setFilteredYear(filteredYear);
  };

  const matchedItems = items.filter(
    (expense) => String(expense.date.getFullYear()) === filteredYear,
  );

  return (
    <div>
      <Card className='expenses'>
        <ExpensesFilter
          selectedYear={filteredYear}
          onChangeHandler={filterChangeHandler}
        />
        {matchedItems.length === 0 ? (
          <p>No expenses found.</p>
        ) : (
          matchedItems.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))
        )}
      </Card>
    </div>
  );
}

export default Expenses;
```

###  使用 兩個條件式 && 滿足條件式會有的渲染內容  來構成

在這裡使用了
```
{matchedItems.length === 0 && <p>No expenses found.</p>}
```
和
```
        {matchedItems.length > 0 &&
          matchedItems.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))}
```
這兩個條件式 && 滿足條件式會有的渲染內容來組裝成以下內容：

```
import ExpenseItem from './ExpenseItem';
import ExpensesFilter from './ExpensesFilter';
import Card from '../UI/Card';
import { useState } from 'react';
import './Expenses.css';

function Expenses(props) {
  const { items } = props;
  const [filteredYear, setFilteredYear] = useState('2020');

  const filterChangeHandler = (filteredYear) => {
    setFilteredYear(filteredYear);
  };

  const matchedItems = items.filter(
    (expense) => String(expense.date.getFullYear()) === filteredYear,
  );

  return (
    <div>
      <Card className='expenses'>
        <ExpensesFilter
          selectedYear={filteredYear}
          onChangeHandler={filterChangeHandler}
        />
        {matchedItems.length === 0 && <p>No expenses found.</p>}
        {matchedItems.length > 0 &&
          matchedItems.map((expense) => (
            <ExpenseItem
              key={expense.id}
              title={expense.title}
              amount={expense.amount}
              date={expense.date}
            />
          ))}
      </Card>
    </div>
  );
}

export default Expenses;

```


### 從渲染層面移除條件判斷


在這裡從渲染部分切分出條件式處理的部分，並以處理結果作為主要的渲染結果：
```
  let expensesContent = <p>No expenses found.</p>;

  if (matchedItems.length > 0) {
    expensesContent = matchedItems.map((expense) => (
      <ExpenseItem
        key={expense.id}
        title={expense.title}
        amount={expense.amount}
        date={expense.date}
      />
    ));
  }
```



```
import ExpenseItem from './ExpenseItem';
import ExpensesFilter from './ExpensesFilter';
import Card from '../UI/Card';
import { useState } from 'react';
import './Expenses.css';

function Expenses(props) {
  const { items } = props;
  const [filteredYear, setFilteredYear] = useState('2020');

  const filterChangeHandler = (filteredYear) => {
    setFilteredYear(filteredYear);
  };

  const matchedItems = items.filter(
    (expense) => String(expense.date.getFullYear()) === filteredYear,
  );

  let expensesContent = <p>No expenses found.</p>;

  if (matchedItems.length > 0) {
    expensesContent = matchedItems.map((expense) => (
      <ExpenseItem
        key={expense.id}
        title={expense.title}
        amount={expense.amount}
        date={expense.date}
      />
    ));
  }
  return (
    <div>
      <Card className='expenses'>
        <ExpensesFilter
          selectedYear={filteredYear}
          onChangeHandler={filterChangeHandler}
        />
        {expensesContent}
      </Card>
    </div>
  );
}

export default Expenses;
```

## 複習


---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: