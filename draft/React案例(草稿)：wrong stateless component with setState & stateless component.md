前者本身就沒有狀態更新的函式來根據使用者輸入來更新，因此會出現不一致情況
```
import './ExpenseItem.css';

import Card from '../UI/Card';

import ExpenseDate from './ExpenseDate';

import { useState } from 'react';

  

function ExpenseItem(props) {

const [title, setTitle] = useState(props.title);

  

const clickHandler = (event) => {

setTitle('updated!!');

};

return (

<Card className='expense-item' id={props.id}>

<ExpenseDate date={props.date} />

<div className='expense-item__description'>

<h2>{title}</h2>

<div className='expense-item__price'>{props.amount}</div>

</div>

<button onClick={clickHandler}>test btn</button>

</Card>

);

}

  

export default ExpenseItem;

```







```

import './ExpenseItem.css';

import Card from '../UI/Card';

import ExpenseDate from './ExpenseDate';

  

function ExpenseItem(props) {

const { date, title, id } = props;

  

return (

<Card className='expense-item' id={id}>

<ExpenseDate date={date} />

<div className='expense-item__description'>

<h2>{title}</h2>

<div className='expense-item__price'>{props.amount}</div>

</div>

</Card>

);

}

  

export default ExpenseItem;
```