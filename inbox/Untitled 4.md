## 描述


```
### 2.1 语法

useImperativeHandle(ref, createHandle, [deps])

1.  `ref`  
    需要被赋值的`ref`对象。
2.  `createHandle`：  
    `createHandle`函数的返回值作为`ref.current`的值。
3.  `[deps]`  
    依赖数组，依赖发生变化会重新执行`createHandle`函数。
```


## 複習


---
Status: #🌱 #📓 
Tags:
Links:
References: