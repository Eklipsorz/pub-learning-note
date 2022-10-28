
## 描述
[[@wikidataJingZhengWeiHai2022]] 描述
> **競爭危害**（race hazard）又名**競態條件**、**競爭條件**（race condition），它旨在描述一個系統或者進程的輸出依賴於不受控制的事件出現順序或者出現時機。此詞源自於兩個訊號試著彼此競爭，來影響誰先輸出。

> 舉例來說，如果電腦中的兩個行程同時試圖修改一個共享記憶體的內容，在沒有並行控制的情況下，最後的結果依賴於兩個行程的執行順序與時機。而且如果發生了並行存取衝突，則最後的結果是不正確的。
> 
> 競爭危害常見於不良設計的電子系統，尤其是邏輯電路。但它們在軟體中也比較常見，尤其是有採用多執行緒技術的軟體。

[[@RaceCondition2022]] 描述：
> A **race condition** or **race hazard** is the condition of an electronics, software, or other system where the system's substantive behavior is dependent on the sequence or timing of other uncontrollable events. It becomes a bug when one or more of the possible behaviors is undesirable.

[[@techtargetWhatRaceCondition]] 描述：
> A race condition is an undesirable situation that occurs when a device or system attempts to perform two or more operations at the same time, but because of the nature of the device or system, the operations must be done in the proper sequence to be done correctly.




重點：
- race condition 是指多個程式模組以不受控制的執行順序來彼此競爭著改變最後結果的狀態，使結果不如開發者所預期的結果，不受控制的執行順序包含了以下：
	- 多個程式模組的同時執行：由於同時執行著多個程式模組，導致系統和開發者難以知道其執行順序是如何，使其很難透過控制其順序來使結果如同開發者所想要的結果
- 為什麼多個程式模組的序列無法構成不受控制的執行順序？
	- 當多個程式模組排隊著去執行時，肯定只有少部分或者還沒有程式模組去被執行，而大部分程式模組就已經在隊伍等候執行，其隊伍結構本身就可以讓系統和開發者先被了解，因此可以先調整隊伍中的程式模組使它們能讓結果如同開發者所想要的結果
- 通常這些程式模組能夠影響最後結果方式：
	- 競爭存取著同一份資料、資源，而這些資料、資源將會影響結果


### 為什麼多個程式模組的序列無法構成不受控制的執行順序？
當多個程式模組排隊著去執行時，肯定只有少部分或者還沒有程式模組去被執行，而大部分程式模組就已經在隊伍等候執行，其隊伍結構本身就可以讓系統和開發者先被了解，因此可以先調整隊伍中的程式模組使它們能讓結果如同開發者所想要的結果

### race condition 命名緣由
race 原意為競爭，condition 是指狀態、狀況，在電腦科學是指多個程式模組在彼此競爭誰能夠影響最後結果
- 若是序列執行，那就是多個程式模組排隊影響最後結果
- 若是並列執行，那就是多個程式模組同時執行，並且不排隊，直接誰先搶到誰就先影響
## 複習


#🧠 race condition 是指什麼？哪種情況會衍生？->->-> `是指多個程式模組以不受控制的執行順序來彼此競爭著改變最後結果的狀態，使結果不如開發者所預期的結果，不受控制的執行順序包含了以下： - 多個程式模組的同時執行：由於同時執行著多個程式模組，導致系統和開發者難以知道其執行順序是如何，使其很難透過控制其順序來使結果如同開發者所想要的結果`
<!--SR:!2022-12-17,80,208-->


#🧠 race condition：為什麼多個程式模組的序列無法構成不受控制的執行順序 ->->-> `當多個程式模組排隊著去執行時，肯定只有少部分或者還沒有程式模組去被執行，而大部分程式模組就已經在隊伍等候執行，其隊伍結構本身就可以讓系統和開發者先被了解，因此可以先調整隊伍中的程式模組使它們能讓結果如同開發者所想要的結果`
<!--SR:!2023-05-07,191,250-->


#🧠 race condition 是指多個程式模組以不受控制的執行順序來彼此競爭著最後的結果，使結果不如開發者所預期的結果，不受控制的執行順序包含了哪些？ 為什麼？ ->->-> `多個程式模組的同時執行：由於同時執行著多個程式模組，導致系統和開發者難以知道其執行順序是如何，很難透過控制其順序來使結果如同開發者所想要的結果`
<!--SR:!2022-11-25,76,230-->

#🧠 race condition：為什麼多個程式模組能夠影響最後結果，通常會是什麼？(資料會影響結果嗎) ->->-> `多個程式模組都競爭存取著同一份資料、資源，而這些資料、資源將會影響結果`
<!--SR:!2022-11-18,78,230-->


#🧠  race condition：多個程式模組能夠影響最後結果，若多個程式並列執行的話，會是如何執行？->->-> `那就是多個程式模組同時執行，並且不排隊，直接誰先搶到誰就先影響`
<!--SR:!2022-11-16,78,230-->


#🧠 race condition 命名緣由 ->->-> `race 原意為競爭，condition 是指狀態、狀況，在電腦科學是指多個程式模組在彼此競爭誰能夠影響最後結果`
<!--SR:!2023-04-30,185,250-->

---
Status: #☀️ 
Tags:
[[Operating System]]
Links:
References:
[[@techtargetWhatRaceCondition]]
[[@RaceCondition2022]]
[[@wikidataJingZhengWeiHai2022]]
