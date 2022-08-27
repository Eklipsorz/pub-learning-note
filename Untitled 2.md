## 描述

由於Expenses元件越來越臃腫，在這裡會額外建立一個ExpenseList

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

### 將原本有條件式邏輯判斷的元件A拆分成一個專門依照條件式來回傳渲染內容的元件

將原本有條件式邏輯判斷的元件A拆分成一個專門依照條件式來回傳渲染內容的元件以及被拆掉條件式的元件A


```
// 專門依照條件式來回傳渲染內容的元件
import './ExpenseList.css';
import ExpenseItem from './ExpenseItem';
function ExpenseList(props) {
  const { items } = props;
  if (!items.length) {
    return <h2 className='expenses-list__fallback'>Found no expenses.</h2>;
  }

  return (
    <ul className='expenses-list'>
      {items.map((expense) => (
        <ExpenseItem
          key={expense.id}
          title={expense.title}
          amount={expense.amount}
          date={expense.date}
        />
      ))}
    </ul>
  );
}

export default ExpenseList;

```


```
// 拆掉條件式的元件A
import ExpensesFilter from './ExpensesFilter';
import ExpenseList from './ExpenseList';
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
        <ExpenseList items={matchedItems} />
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