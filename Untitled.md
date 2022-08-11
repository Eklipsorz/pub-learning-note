## 描述

### 修改前
ExpenseItem.js
```
import './ExpenseItem.css';
import ExpenseDate from './ExpenseDate';

function ExpenseItem(props) {
	const month = props.date.toLocaleString('en-US', { month: 'long' });
	const day = props.date.toLocaleString('en-US', { day: '2-digit' });
	const year = props.date.getFullYear();
	
	return (
		<div className='expense-item' id={props.id}>
			<div className='expense-date'>
				<div className='expense-date__month'>{month}</div>
				<div className='expense-date__year'>{year}</div>
				<div className='expense-date__day'>{day}</div>
			</div>
			<div className='expense-item__description'>
				<h2>{props.title}</h2>
				<div className='expense-item__price'>{props.amount}</div>
			</div>
		</div>
	);
}

export default ExpenseItem;
```

### 修改後

ExpenseItem.js
```
import './ExpenseItem.css';
import ExpenseDate from './ExpenseDate';

function ExpenseItem(props) {

	return (
		<div className='expense-item' id={props.id}>
			<ExpenseDate date={props.date} />
			<div className='expense-item__description'>
				<h2>{props.title}</h2>
				<div className='expense-item__price'>{props.amount}</div>
			</div>
		</div>
	);
}

export default ExpenseItem;
```


ExpenseDate.js
```
import './ExpenseDate.css';
 
function ExpenseDate(props) {

	const month = props.date.toLocaleString('en-US', { month: 'long' });
	const day = props.date.toLocaleString('en-US', { day: '2-digit' });
	const year = props.date.getFullYear();

	return (
		<div className='expense-date'>
			<div className='expense-date__month'>{month}</div>
			<div className='expense-date__year'>{year}</div>
			<div className='expense-date__day'>{day}</div>
		</div>
	);

}

export default ExpenseDate;
```


## 複習
#🧠 Question :: ->->-> ``

---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
References: