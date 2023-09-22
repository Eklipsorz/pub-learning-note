## 描述

[[@wikidataSideEffectComputer2022]] 所描述：
> In computer science, an operation, function or expression is said to have a side effect if it modifies some state variable value(s) outside its local environment, which is to say if it has any observable effect other than its primary effect of returning a value to the invoker of the operation. 

[[@wikidataFuZuoYongJiSuanJiKeXue2022]] 所描述：
> 在電腦科學中，函數副作用指當調用函數時，除了返回可能的函數值之外，還對主調用函數產生附加的影響。例如修改全域變數（函數外的變數），修改參數，向主調方的終端、管道輸出字符或改變外部存儲資訊等。 

重點：
- Side Effect 為執行主要處理(結果)所會帶來的任意額外處理(結果)，在電腦科學會是指
	- 當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了做完主要效果以外，還帶來另一個任意額外處理，那麼代表操作/表達式/函式是擁有side effect，而任意額外處理就是side effect
	- 主要效果會是指：回傳結果給調用者
	- 任意額外處理通常會是影響主調用者所使用的共享資源，比如修改全域變數、共享用的資源
- Side Effect 在電腦科學裡主要是形容特定操作、表達式、函式


### effect 命名緣由

> the result of a particular influence

重點：
- effect 指特定處理的結果
### side effect 命名緣由

> an unexpected result of a situation

重點：
-  Side Effect 為執行主要處理(結果)所會帶來的任意額外處理(結果)，其任意額外處理(結果)可以是
	- 預期外
	- 預期內



## 複習
#🧠 effect 命名緣由 ->->-> `effect 指特定處理的結果`
<!--SR:!2024-06-13,303,230-->


#🧠 side effect 命名緣由 (說到預期內和預期外) ->->-> `Side Effect 為執行主要處理(結果)所會帶來的任意額外處理(結果)，其任意額外處理(結果)可以是預期外或者預期內`
<!--SR:!2024-11-13,448,250-->


#🧠 side effect 命名緣由 ->->-> `Side Effect 為執行主要處理(結果)所會帶來的任意額外處理(結果)，其任意額外處理(結果)可以是預期外或者預期內`
<!--SR:!2023-11-11,90,230-->


#🧠 side effect 在電腦科學裡是泛指什麼意思？ ->->-> ` 當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了做完主要效果以外，還帶來另一個任意額外處理，那麼代表操作/表達式/函式是擁有side effect，而任意額外處理就是side effect`
<!--SR:!2024-09-09,413,250-->

#🧠  side effect 在電腦科學裡是泛指當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了做完主要效果以外，還帶來另一個任意額外處理，那麼代表操作/表達式/函式是擁有side effect，而任意額外處理就是side effect，其中的主要效果和任意額外處理通常會泛指著什麼？->->-> `前者會是指將結果回傳給主調用者；後者則是影響主調用者所會使用到的共享資源或者記憶體`
<!--SR:!2024-08-01,374,250-->


#🧠 什麼樣的操作/表達式/函式會是具有side effect的操作/表達式/函式？ ->->-> `當調用者執行特定操作/表達式/函式時，這些操作/表達式/函式除了回傳值給調用者這個主要效果以外，還出現其他任何一個可觀察到的效果(effect)，那麼代表操作/表達式/函式是擁有side effect`
<!--SR:!2023-11-09,88,230-->


#🧠 Side Effect 在電腦科學上是泛指著除了主要效果以外的額外效果，其中的額外效果是包含了什麼種類？(能不能想得到)->->-> `是泛指著除了主要效果以外的額外效果，其中的額外效果會是包含預期額外效果、預期外額外效果`
<!--SR:!2024-02-11,219,230-->


#🧠 Side Effect 在電腦科學上是泛指著除了主要效果以外的額外效果，其中主要效果是什麼？->->-> `是回傳值給調用者`
<!--SR:!2023-09-29,183,230-->



#🧠 Side Effect 在電腦程式開發裡通常會是什麼樣的效果？ ->->-> `side effect 通常會是影響主調用者所使用的共享資源之效果`
<!--SR:!2023-12-04,73,210-->



#🧠 side effect 會用來形容誰？ ->->-> `函式、特定操作、表達式`
<!--SR:!2024-10-26,438,250-->




---
Status: #🌱 
Tags
[[Operating System]] - [[useEffect]]
Links:
References:
[[@wikidataSideEffectComputer2022]]
[[@wikidataFuZuoYongJiSuanJiKeXue2022]]