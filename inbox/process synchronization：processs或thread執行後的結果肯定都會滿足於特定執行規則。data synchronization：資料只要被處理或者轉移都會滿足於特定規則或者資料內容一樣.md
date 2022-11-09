
## 描述


### Synchronization 
[[@wikidataSynchronizationComputerScience2022]]
> In computer science, synchronization refers to one of two distinct but related concepts: synchronization of processes, and synchronization of data.

重點：
- synchronization在電腦科學上可區分成：
	- process synchronization：多個process/thread相互協調執行方式，使他們在特定層面下的結果會是一樣
	- data synchronization：
	- 多個 data 處理相互協調資料如何處理，使他們在他們在特定層面下的結果會是一樣




###  Data Synchronization
[[@wikidataSynchronizationComputerScience2022]]
> Data synchronization is the process of establishing consistency between source and target data stores, and the continuous harmonization of the data over time. It is fundamental to a wide variety of applications, including file synchronization and mobile device synchronization.

重點：
- 多個 data 處理相互協調資料如何處理，使他們在他們在特定層面下的結果會是一樣
	- 特定層面通常會是指處理後的資料是否還是一樣或者是否滿足特定規則
- 資料處理本身可以分為資料轉移、資料處理，若搭配常見的特定層面
	- 資料轉移：從資料來源處和資料目標存放處之間的轉移處理中，
- 資料只要被處理或者轉移都會滿足於特定規則或者資料內容一樣
- 資料同步：是指在資料來源處和資料目標存放處之間的轉移處理中 **雙方的同份資料會是一樣內容這目標** 以及 **雙方的同份資料都會是滿足儲存空間對於資料的規則** 這過程


### Process Synchronziation
[[process或者thread synchronization 是指多個process或者thread相互協調執行方式，使他們在特定層面下的結果會是一樣，若一樣的話，則這些process或者thread會是同步的，反之，為非同步。]]

### synchronization 本身含義

synchronize：與特定事物進行協調/處理，使它們在特定層面下的結果是一樣

synchronization ：synchronize 進行過程


## 複習


#🧠 synchronization在電腦科學上可區分成哪兩種？->->-> `Data Synchronization、Process/Thread Synchronization`

#🧠 Data Synchronization 會是指什麼？ ->->-> `資料只要被處理或者轉移都會滿足於特定規則或者資料內容一樣`

#🧠 Data Synchronization 放在來源處和目標處的轉移會是如何說？ ->->-> `是指在資料來源處和資料目標存放處之間的轉移處理中 **雙方的同份資料會是一樣內容這目標** 以及 **雙方的同份資料都會是滿足儲存空間對於資料的規則** 這過程`

#🧠 Process/Thread Synchronization 會是指什麼？: ->->-> `processs/thread執行後的結果肯定都會滿足於特定執行規則`


---
Status: #🌱 
Tags:
[[Operating System]]
Links:
[[process或者thread synchronization 是指多個process或者thread相互協調執行方式，使他們在特定層面下的結果會是一樣，若一樣的話，則這些process或者thread會是同步的，反之，為非同步。]]
References:
[[@wikidataSynchronizationComputerScience2022]]