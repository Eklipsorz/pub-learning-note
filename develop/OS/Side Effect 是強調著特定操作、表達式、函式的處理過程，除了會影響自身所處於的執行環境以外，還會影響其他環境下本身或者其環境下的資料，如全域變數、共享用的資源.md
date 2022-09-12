## 描述

[[@wikidataSideEffectComputer2022]] 所描述：
> In computer science, an operation, function or expression is said to have a side effect if it modifies some state variable value(s) outside its local environment, which is to say if it has any observable effect other than its primary effect of returning a value to the invoker of the operation. 

[[@wikidataFuZuoYongJiSuanJiKeXue2022]] 所描述：
> 在電腦科學中，函數副作用指當調用函數時，除了返回可能的函數值之外，還對主調用函數產生附加的影響。例如修改全域變數（函數外的變數），修改參數，向主調方的終端、管道輸出字符或改變外部存儲資訊等。 

重點：
- 當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了回傳值給調用者這個主要效果以外，還出現其他任何一個可觀察到的效果(effect)，那麼代表操作/表達式/函式是擁有side effect
- 除了回傳值給調用者這個主要效果以外的額外效果，就稱之為side effect，通常會影響主調用者所使用的共享資源，比如修改全域變數、共享用的資源
- Side Effect 主要是形容特定操作、表達式、函式


### effect 命名緣由

> the result of a particular influence

重點：
- effect 是指一個特定影響的結果，在電腦科學可以指特定處理的結果
### side effect 命名緣由

> an unexpected result of a situation

重點：
- side effect 是指一個預期外的結果


## 複習
#🧠 什麼樣的操作/表達式/函式會是具有side effect的操作/表達式/函式？ ->->-> `當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了回傳值給調用者這個主要效果以外，還出現其他任何一個可觀察到的效果(effect)，那麼代表操作/表達式/函式是擁有side effect`



#🧠 Side Effect 是什麼？ ->->-> `特定操作、表達式、函式的處理過程，除了會影響自身所處於的執行環境以外，還會影響其他環境下本身或者其環境下的資料，如全域變數、共享用的資源`
<!--SR:!2022-10-10,36,230-->

#🧠 Side Effect 是特定操作、表達式、函式的處理過程，除了會影響自身所處於的執行環境以外，還會影響其他環境下本身或者其環境下的資料，其資料會有什麼？->->-> `全域變數、共享用的資源`
<!--SR:!2022-09-21,28,250-->


---
Status: #🌱 
Tags
[[Operating System]]
Links:
References:
[[@wikidataSideEffectComputer2022]]
[[@wikidataFuZuoYongJiSuanJiKeXue2022]]