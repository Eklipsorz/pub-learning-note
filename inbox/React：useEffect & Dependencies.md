## 描述



### callback 設


### dependency 設定目的
```
useEffect(callback, dependency)
```

1. 定義callback 會用到的變數、狀態、props
2. 給予一個手段來防止effect的觸發執行於每次元件的渲染週期內不會產生出無限循環

### dependency 設定的注意事項

> -   You **DON'T need to add state updating functions** (as we did in the last lecture with `setFormIsValid`): React guarantees that those functions never change, hence you don't need to add them as dependencies (you could though)
    
> -   You also **DON'T need to add "built-in" APIs or functions** like `fetch()`, `localStorage` etc (functions and features built-into the browser and hence available globally): These browser APIs / global functions are not related to the React component render cycle and they also never change
    
> -   You also **DON'T need to add variables or functions** you might've **defined OUTSIDE of your components** (e.g. if you create a new helper function in a separate file): Such functions or variables also are not created inside of a component function and hence changing them won't affect your components (components won't be re-evaluated if such variables or functions change and vice-versa)

重點：
- dependency 不需要添加更新狀態用的函式：因為React本身和使用者本身就不會變動該函式本身
- dependency 不要添加其他非React能夠支援的API 或者對應函式：因為他們本身就不會改變和跟元件渲染週期無關
- dependency 不要添加屬於其他元件或者元件以外的變數/函式，因為它們本身就屬於其他元件或者非元件，它們一改變就無法對目前元件觸發渲染

## 複習

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
[[React：effect 使用方式]]
[[React：effect 是指除了元件本身所要做的主要功能-渲染元件、與使用者互動來管理狀態以外的額外效果，額外效果會是指脫離渲染週期的任意功能]]
References: