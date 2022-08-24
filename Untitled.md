controlled component

this component controls the expenses filter component


> 我們可以透過將 React 的 state 變成「唯一真相來源」來將這兩者結合。如此，render 表單的 React component 同時也掌握了後續使用者的輸入對表單帶來的改變。像這樣一個輸入表單的 element，被 React 用這樣的方式來控制它的值，就被稱為「controlled component」。