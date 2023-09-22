
## 描述


### Synchronization 
[[@wikidataSynchronizationComputerScience2022]]
> In computer science, synchronization refers to one of two distinct but related concepts: synchronization of processes, and synchronization of data.

重點：
- synchronization在電腦科學上可區分成：
	- process synchronization：多個process/thread相互協調執行方式，使他們在特定層面下的結果會是一樣
	- data synchronization：多個 data 處理相互協調資料如何處理，使他們在特定層面下的結果會是一樣



###  Data Synchronization
[[@wikidataSynchronizationComputerScience2022]]
> Data synchronization is the process of establishing consistency between source and target data stores, and the continuous harmonization of the data over time. It is fundamental to a wide variety of applications, including file synchronization and mobile device synchronization.

重點：
- 多個 data 處理相互協調資料如何處理，使他們在他們在特定層面下的結果會是一樣
	- 特定層面通常會是指處理後的資料是否還是一樣或者是否滿足特定規則：
		- 若一樣或者滿足，就會是同步
	- 在這裡場景通常會是指資料轉移部分
- 資料轉移和層面結合會是指
	- 資料轉移：在從資料來源處和資料目標存放處之間的轉移處理中，處理後，雙方的同份資料會是一樣內容或者滿足於特定規則

### Process Synchronziation
[[process或者thread synchronization 是指多個process或者thread相互協調執行方式，使他們在特定層面下的結果會是一樣，若一樣的話，則這些process或者thread會是同步的，反之，為非同步。]]

### synchronization 本身含義

synchronize：與特定事物進行協調/處理，使它們在特定層面下的結果是一樣

synchronization ：synchronize 進行過程


## 複習

#🧠 synchronization在電腦科學上可區分成哪兩種synchronization？->->-> `Data Synchronization、Process/Thread Synchronization`
<!--SR:!2023-11-06,175,230-->

#🧠 Data Synchronization 會是指什麼？ ->->-> `多個 data 處理相互協調資料如何處理，使他們在特定層面下的結果會是一樣`
<!--SR:!2024-06-23,355,250-->

#🧠 Data Synchronization 是多個 data 處理相互協調資料如何處理，使他們在特定層面下的結果會是一樣，那麼常見的場景和特定層面會是什麼？ ->->-> `場景會是資料上的轉。層面會是指處理後的資料是否還是一樣或者是否滿足特定規則`
<!--SR:!2023-11-21,90,230-->

#🧠 在Data Synchronization 中，搭配著資料轉移這資料場景以及常見特定層面的話，會組合成什麼意思？ ->->-> `在從資料來源處和資料目標存放處之間的轉移處理中，處理後，雙方的同份資料會是一樣內容或者滿足於特定規則`
<!--SR:!2024-01-05,197,230-->

#🧠 Synchronize 本身含義為何？ ->->-> `與特定事物進行協調/處理，使它們在特定層面下的結果是一樣`
<!--SR:!2024-09-14,409,250-->

#🧠 在Data Synchronization 中，那麼如何稱之為同步？ ->->-> `在特定層面通常會是指處理後的資料是否還是一樣或者是否滿足特定規則：若一樣或者滿足，就會是同步`
<!--SR:!2025-02-19,516,250-->

#🧠 process/thread synchronization會是指什麼？->->-> `多個process/thread相互協調執行方式，使他們在特定層面下的結果會是一樣`
<!--SR:!2024-03-12,302,250-->

#🧠 Synchronization  本身含義為何？ ->->-> `與特定事物進行協調/處理，使它們在特定層面下的結果是一樣 之過程/行為`
<!--SR:!2024-06-04,348,250-->


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
[[process或者thread synchronization 是指多個process或者thread相互協調執行方式，使他們在特定層面下的結果會是一樣，若一樣的話，則這些process或者thread會是同步的，反之，為非同步。]]
References:
[[@wikidataSynchronizationComputerScience2022]]