## 描述



### 問題1：沒用額外的parent 元件來包覆

> Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment
> adjacent, which means side-by-side JSX elements, must be wrapped in an in closing tag

JSX 元件沒用額外的parent 元件來包覆著

### 問題1案例
```
function Component(props) {

  return (

      <section id="goal-form">
        <CourseInput onAddGoal={addGoalHandler} />
      </section>
      <section id="goals">
        {content}
      </section>

  );
}
```


### 問題2：使用沒定義的識別字

> 'addGoalaHandler' is not defined

使用沒定義的識別字

### 問題2案例

```
import React, { useState } from 'react';

import CourseGoalList from './components/CourseGoals/CourseGoalList/CourseGoalList';
import CourseInput from './components/CourseGoals/CourseInput/CourseInput';
import './App.css';

const App = () => {
  const [courseGoals, setCourseGoals] = useState([
    { text: 'Do all exercises!', id: 'g1' },
    { text: 'Finish the course!', id: 'g2' },
  ]);

  const addGoalHandler = (enteredText) => {
    setCourseGoals((prevGoals) => {
      const updatedGoals = [...prevGoals];
      updatedGoals.unshift({ text: enteredText, id: 'goal1' });
      return updatedGoals;
    });
  };

  const deleteItemHandler = (goalId) => {
    setCourseGoals((prevGoals) => {
      const updatedGoals = prevGoals.filter((goal) => goal.id !== goalId);
      return updatedGoals;
    });
  };

  let content = (
    <p style={{ textAlign: 'center' }}>No goals found. Maybe add one?</p>
  );

  if (courseGoals.length > 0) {
    content = (
      <CourseGoalList items={courseGoals} onDeleteItem={deleteItemHandler} />
    );
  }

  return (
    <div>
      <section id='goal-form'>
        <CourseInput onAddGoal={addGoalaHandler} />
      </section>
      <section id='goals'>{content}</section>
    </div>
  );
};

export default App;

```


### 問題3：邏輯問題

問題：每當新增兩個以上的項目時，對著第一個項目點擊刪除時，總會刪到其他項目

#### 檢測方法1
1. 先遍歷定義刪除邏輯的部份來找到真正錯誤的地方，在這裡會追溯至App.js的deleteItemHandler：
	- 遍歷過程：CourseGoalItem -> CourseGoalList -> App.js
2. 確定deleteItemHandler沒問題，就去看看新增項目時或者賦予id的地方會有什麼問題


#### 檢測方法2

觀看瀏覽器給予的資訊：
- 增加第一個項目後，並不會出現以下訊息，直到增加第二個項目後，就產生以下訊息：
> Warning: Encountered two children with the same key, `goal1`. Keys should be unique so that components maintain their identity across updates. Non-unique keys may cause children to be duplicated and/or omitted — the behavior is unsupported and could change in a future version.



### 如果IDE能夠偵測到錯誤，通常會是語法錯誤



## 複習
#🧠 如果React 專案出現以下訊息：Adjacent JSX elements must be wrapped in an enclosing tag. Did you want a JSX fragment adjacent, which means side-by-side JSX elements, must be wrapped in an in closing tag ，這代表什麼？->->-> `JSX 元件沒用額外的parent 元件來包覆著`
<!--SR:!2024-01-13,302,250-->

#🧠 如果React 專案出現以下訊息：'addGoalaHandler' is not defined，這代表什麼？ ->->-> `使用沒定義的識別字`
<!--SR:!2023-11-28,93,230-->


---
Status: #🌱 
Tags:
[[React]]
Links:
References: