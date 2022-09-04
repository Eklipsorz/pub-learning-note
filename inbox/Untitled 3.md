## 描述



### 問題1

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


### 問題2 

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

### 如果IDE能夠偵測到錯誤，通常會是語法錯誤



## 複習


---
Status: #🌱 
Tags:
[[React]]
Links:
References: