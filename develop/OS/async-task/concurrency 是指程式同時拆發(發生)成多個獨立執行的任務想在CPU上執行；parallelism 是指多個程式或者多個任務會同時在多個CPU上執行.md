## 描述

[[@BingfaConcurrencyYubinghang]]
> 在英文中，con意为“一起,”(with, together)，而cur表示“跑”(run)的意思，因此两者合起来Concurrency就是同时开始跑，即同时发生的意思。在parallelism可以拆分为par+all（=other)，其中par意为并列或者肩并肩(side by side），合起来表示相互不同的多个东西并列存在。


> 顾名思义，并发是同时发生，并行就是同时执行。在中文中，并发的字面意思指的是线程同时开始执行这个事件，也就是说后续的执行是串行，还是并行，不确定，依赖于底层的硬件条件和操作系统的调度，而并行则指的是线程同时执行这个过程。



> 无论是中文，还是英文，从字面意思而言，并发表示线程同时开始，代表的是事件，而并行表示线程同时执行，代表的是过程或者活动。

[[@GaiNianHackMD]]
> **Concurrency** 是指程式架構，將程式拆開成多個可獨立運作的工作。案例: 裝置驅動程式，可獨立運作，但不需要平行化。

> -   拆開多個的工作不一定要同時運行
> -   多個工作在單核 CPU 上運行

![](https://hackpad-attachments.s3.amazonaws.com/embedded2016.hackpad.com_K6DJ0ZtiecH_p.537916_1460613316743_p1.png)


> **Parallelism:** 是指程式執行，同時執行多個程式。Concurrency 可能會用到 parallelism，但不一定要用 parallelism 才能實現 concurrency。eg：Vector dot product

> -   程式會同時執行 (如：fork 後，同時執行，再收集結果，即 join 操作)
> -   一個工作在多核處理器上運作

![](https://hackpad-attachments.s3.amazonaws.com/embedded2016.hackpad.com_K6DJ0ZtiecH_p.537916_1460613329719_p2.png)

重點：
- concurrency 原意為同時發生，在電腦科學裡是指同時發生多個任務想要執行在CPU中，實作上是指程式執行架構，該架構將程式同時拆分成多個獨立執行的任務來執行。
	- 每個獨立的任務不一定會同時執行
	- 在單核CPU上運行，每個任務會輪流使用CPU來執行；在多核心CPU上運行，每個任務會存在各個核心上來同時執行

- parallelism 原意為多個事物並列存在，在電腦科學裡是指多個程式會同時存在CPU中，實作中會是指多個程式會同時被執行
	- 存在多核心CPU上運行
	- 每個任務或者每個程式肯定會同時存在各個核心來執行各自任務


### concurrency 命名緣由 && parallelism 命名緣由

> 在英文中，con意为“一起,”(with, together)，而cur表示“跑”(run)的意思，因此两者合起来Concurrency就是同时开始跑，即同时发生的意思。在parallelism可以拆分为par+all（=other)，其中par意为并列或者肩并肩(side by side），合起来表示相互不同的多个东西并列存在。

重點：
- concurrency 表明為 con 為一起的意思，cur為跑的意思，兩者合起來同時開始跑，即同時發生
- parallelism 表明par+all (side by side + other) 與多個事物並列存在，即多個事物並列存在


## 複習

#🧠 concurrency 命名緣由為何？ ->->-> `concurrency 表明為 con 為一起的意思，cur為跑的意思，兩者合起來同時開始跑，即同時發生`
<!--SR:!2023-11-30,190,250-->

#🧠 parallelism 命名緣由為何？ ->->-> ` parallelism 表明par+all (side by side + other) 與多個事物並列存在，即多個事物並列存在`
<!--SR:!2024-02-19,225,230-->

#🧠 concurrency 原意為同時發生，在電腦科學中會是指什麼，其實作概念又會是什麼？->->-> `在電腦科學裡是指同時發生多個任務想要執行在CPU中，實作上是指程式執行架構，該架構將程式同時拆分成多個獨立執行的任務來執行`
<!--SR:!2023-07-23,112,248-->

#🧠 concurrency 在電腦科學裡是指同時發生多個任務想要執行在CPU中，實作上是指程式執行架構，該架構將程式同時拆分成多個獨立執行的任務來執行，其任務的執行模式是什麼？  以單核心和多核心為例->->-> `	- 每個獨立的任務不一定會同時執行 - 在單核CPU上運行，每個任務會輪流使用CPU來執行；在多核心CPU上運行，每個任務會存在各個核心上來同時執行`
<!--SR:!2023-07-30,105,228-->

#🧠 parallelism 在電腦科學裡是指多個程式會同時存在CPU中，實作中會是指多個程式會同時被執行，其任務的執行模式是什麼？  以單核心和多核心為例 ->->-> `	- 存在多核心CPU上運行 - 每個任務或者每個程式肯定會同時存在各個核心來執行各自任務`
<!--SR:!2024-03-11,246,248-->

#🧠 parallelism 原意為與多個事物並列存在，在電腦科學中會是指什麼，其實作概念又會是什麼？ ->->-> `在電腦科學裡是指多個程式會同時存在CPU中，實作中會是指多個程式會同時被執行`
<!--SR:!2024-03-30,265,250-->


---
Status: #🌱 
Tags:

Links:
References:
[[@GaiNianHackMD]]
[[@BingfaConcurrencyYubinghang]]