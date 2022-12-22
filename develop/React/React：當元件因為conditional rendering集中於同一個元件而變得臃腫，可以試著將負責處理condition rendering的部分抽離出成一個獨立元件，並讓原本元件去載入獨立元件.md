## 描述

當元件因為conditional rendering集中於同一個元件而變得臃腫，可以試著將負責處理condition rendering的部分抽離出成一個獨立元件，並讓原本元件去載入獨立元件。

### 例子
當Expenses元件因為conditional rendering集中於同一個元件而變得臃腫，就會將conditional rendering部分獨立被抽離成立另一個名為ExpenseList.js


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

#### 將原本有條件式邏輯判斷的元件A拆分成一個專門依照條件式來回傳渲染內容的元件

將原本有條件式邏輯判斷的Expenses.js拆分成一個專門處理conditional rendering的ExpenseList.js以及被拆掉條件式的Expenses.js


```
// ExpenseList.js
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
// Expenses.js
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

#🧠 React：conditional rendering 若不想將集中一個元件的話，可以怎麼做 ->->-> `試著從該元件的condition rendering部分抽離出來成一個獨立元件，並讓獨立元件載入至原元件`
<!--SR:!2023-07-01,191,250-->


#🧠  React：試著將下面的condition rendering抽離出成獨立元件來呈現 ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661693270/blog/react/conditional-rendering/conditional-rendering-before-example_o3pacr.png) ->->-> `![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661693269/blog/react/conditional-rendering/conditional-rendering-after-ExpenseList.js_s4dqvd.png) ![](https://res.cloudinary.com/dqfxgtyoi/image/upload/v1661693269/blog/react/conditional-rendering/conditional-rendering-after-expenses.js_fcd1ko.png)` `
<!--SR:!2023-01-29,39,230-->



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：conditional rendering 是根據執行狀態來調整渲染內容的技術]]
[[React： JSX parser 從JSX語法解析{}時，會從JSX parser換成JS引擎來以expression形式執行{}內的內容]]
References: