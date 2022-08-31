
## 描述



### 元件間的互動
1. 由Expenses/Expenses.js 傳遞每一年的開支至Expenses/ExpenseChart.js
2. Expenses/ExpenseChart.js 元件接收parent 給予的資訊來計算當前年度下的每個月的開支以及最高開支，把每個月開支和最高開支傳遞至Chart/Chart.js元件
3. Chart/Chart.js 元件接收資訊並依據月數來產出對應的Chart/ChartBar.js元件，並傳遞資訊至ChartBar.js元件
4. ChartBar.js元件根據資訊來刷新每一個月的開支和標籤的對應畫面

### Expenses/Expenses.js
```
import ExpensesFilter from './ExpensesFilter';
import ExpenseList from './ExpenseList';
import Card from '../UI/Card';
import ExpenseChartBar from './ExpenseChartBar';
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
        <ExpenseChartBar expenses={matchedItems} />
        <ExpenseList items={matchedItems} />
      </Card>
    </div>
  );
}

export default Expenses;

```


### Expenses/ExpenseChart.js

```
import Chart from '../Chart/Chart';
function ExpenseChartBar(props) {
  const { expenses } = props;
  const chartDataPoints = [
    { label: 'Jan', value: 0, maxValue: 0 },
    { label: 'Feb', value: 0, maxValue: 0 },
    { label: 'Mar', value: 0, maxValue: 0 },
    { label: 'Apr', value: 0, maxValue: 0 },
    { label: 'May', value: 0, maxValue: 0 },
    { label: 'Jun', value: 0, maxValue: 0 },
    { label: 'Jul', value: 0, maxValue: 0 },
    { label: 'Aug', value: 0, maxValue: 0 },
    { label: 'Sep', value: 0, maxValue: 0 },
    { label: 'Oct', value: 0, maxValue: 0 },
    { label: 'Nov', value: 0, maxValue: 0 },
    { label: 'Dec', value: 0, maxValue: 0 },
  ];

  // calculate each expense
  for (const expense of expenses) {
    const month = expense.date.getMonth();
    chartDataPoints[month].value += expense.amount;
  }

  // get maximum between expenses
  const values = chartDataPoints.map((point) => point.value);
  const maxValue = Math.max(...values);

  for (const point of chartDataPoints) {
    point.maxValue = maxValue;
  }

  return <Chart dataPoints={chartDataPoints} />;
}

export default ExpenseChartBar;
```


### Chart/Chart.js

chart 元件分成 chart 本身和 顯示每個月開支的chartbar

chart 本身：Chart.js
ChartBar ： ChartBar.js
由Chart.js負責傳遞每個月的資訊至ChartBar.js元件，由該元件渲染指定月份的畫面


```
import './Char.css';
import ChartBar from './ChartBar';
function Chart(props) {
  const { dataPoints } = props;
  return (
    <div className='chart'>
      {dataPoints.map((dataPoint) => (
        <ChartBar
          key={dataPoint.label}
          value={dataPoint.value}
          label={dataPoint.label}
          maxValue={dataPoint.maxValue}
        />
      ))}
    </div>
  );
}

export default Chart;
```

### Chart/ChartBar.js
```
import './ChartBar.css';

function ChartBar(props) {
  const { value, label, maxValue } = props;
  let barFillHeight = '0%';

  if (maxValue > 0) {
    barFillHeight = Math.round((value / maxValue) * 100) + '%';
  }

  return (
    <div className='char-bar'>
      <div className='chart-bar__inner'>
        <div
          className='chart-bar__fill'
          style={{ height: barFillHeight }}
        ></div>
      </div>
      <div className='chart-bar__label'>{label}</div>
    </div>
  );
}

export default ChartBar;
```

#### 圖表的建立

第一層div裡面分別有圖表欄(圖)和圖表欄位標籤這兩個區塊

圖表欄(圖)：具體是用完整bar想呈現哪一個區塊是未填滿的bar部分 以及 哪一個區塊是填滿的bar部分，其中代表填滿的部分則是用barFillHeight變數儲存的值來表示其高度以此表現填滿程度增減

- 計算barFillHeight
```
	const { value, label, maxValue } = props;
	let barFillHeight = '0%';
	
	  
	
	if (maxValue > 0) {
		barFillHeight = Math.round((value / maxValue) * 100) + '%';
	}
```


- 利用barFillHeight來刷新填滿部分的高度。
```
     <div className='chart-bar__inner'>
        <div
          className='chart-bar__fill'
          style={{ height: barFillHeight }}
        ></div>
     </div>
```

圖表欄位標籤：則是以標註著這個bar是代表什麼資料
```
<div className="chart-bar">
	<div className="chart-bar__inner">
		<div className="chart-bar__fill" />
	</div>
	<div className="chart-bar__label">{props.label}</div>
</div>
```



---
Status: #🌱 
Tags:
[[React]] - [[JavaScript]]
Links:
[[React：使用dynamic inline style 來根據執行情況於元件下設定該元件的style]]
References: