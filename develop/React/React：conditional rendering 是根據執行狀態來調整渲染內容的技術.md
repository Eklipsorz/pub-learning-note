## 描述


>condition content
> 1. it's about rendering different output under different conditions

> # Conditional Rendering
> In React, you can create distinct components that encapsulate behavior you need. Then, you can render only some of them, depending on the state of your application.


重點：
- Conditional Rendering 是根據執行情況來調整渲染內容的技術
-  具體有幾種形式：
	1. 使用 條件式 ? 滿足條件式會有的渲染內容 :  不滿足下會有的渲染內容 來構成
	2. 使用 兩個條件式 && 滿足條件式會有的渲染內容 來構成
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

#🧠 Conditional Rendering 在React是什麼？ ->->-> `是根據執行情況來調整渲染內容的技術`
<!--SR:!2022-09-11,10,250-->

#🧠 React：具體實現Conditional Rendering 的手段是什麼？->->-> `使用 條件式 ? 滿足條件式會有的渲染內容、使用 兩個條件式 && 滿足條件式會有的渲染內容來構成、從渲染層面移除條件判斷，在元件的業務邏輯下設定條件來指定要輸出的內容，並於渲染層級以輸出結果來渲染`
<!--SR:!2022-09-12,10,250-->


#🧠 React：請用程式碼來展示Conditional Operator 如何實現Conditional Rendering  ->->-> `return ({enable ? <h1>enable</h1> : <h1>disable</h1>});`
<!--SR:!2022-09-10,9,250-->

#🧠 React：請用程式碼來展示兩個And Operator 如何實現Conditional Rendering ->->-> `return ({enable && <h1>enable</h1>} {!enable && <h1>disable</h1>})`
<!--SR:!2022-09-10,9,250-->


#🧠 React：為何不能夠在JSX語法直接添加if-else語法？而是改用operator ->->-> `因為JSX是由JS和XML所構成，其中JS只允許在{}內執行，在那裡只會被JS引擎當作是expression來執行，而不能以statement，這造成身為statement的if-else不能夠參與，只有能夠被當成expression來執行的operator才行`
<!--SR:!2022-09-29,20,250-->

#🧠  React：請用程式碼來展示渲染層面移除條件判斷，在元件的業務邏輯下設定條件來指定要輸出的內容，並於渲染層級以輸出結果來渲染來 實現Conditional Rendering  ->->-> `let content = <h1>disable</h1> if(enable) content = <h1>enable</h1> return ({content});`
<!--SR:!2022-09-16,12,248-->

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React： JSX parser 從JSX語法解析{}時，會從JSX parser換成JS引擎來以expression形式執行{}內的內容]]
References: