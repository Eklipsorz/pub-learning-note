## 描述

[[@ithomeDay04DOM]]
> 你可以想像 Virtual DOM 就像是畫面產生的模擬彩排場，每次有新 UI 畫面產生的需求時，我們可以用以下流程來完成畫面更新：

> 1.  **透過事先定義好的模板程式來產生新的 Virtual DOM Tree ，作為新的彩排結果**
> 2.  **並且與此前最後一次舊畫面用的 Virtual DOM Tree 進行兩棵樹的結構細節比較，其中差異之處才是本次畫面更新中真正有需要變更的部分**
> 3.  將新舊 Virtual DOM Tree 中有差異的部分更新到真實的 DOM Tree 中，以完成瀏覽器畫面的更新

> 透過這個流程，我們就可以將真實的 DOM 操作範圍最小化，並限縮在這些真正需要變更的地方，來盡可能的減少因 DOM 操作而造成的效能花費。

![](https://miro.medium.com/max/1400/1*ZXE-64hJcWYfNjmWAjiRmw.png)



[[@qianduanmiVirtualDomHeDiffSuanFaTengXunYunKaiFaZheSheQuTengXunYun]]
![](https://ask.qcloudimg.com/http-save/yehe-3615838/w5t0r1qd60.jpeg?imageView2/2/w/1620)

重點：
- Virtual DOM 中的 diffing/ diff algorithm是定義如何比對Virtual DOM之間差異的算法，在這裡會是得到差異
- Virtual DOM 中的 patch algorithm 則是定義如何將差異轉換成對應Real DOM來更新DOM Tree的算法



### Diff 命名緣由

- diff 單純意思

> short for difference 

noun
> The difference between two things is the way in which they are unlike each other.


- 電腦科學的意思

[[@wikidataDiff2022]]
> In computing, the utility diff is a data comparison tool that computes and displays the differences between the contents of files

> Typically, _diff_ is used to show the changes between two versions of the same file

> The utility displays the changes in one of several standard formats, such that both humans or computers can parse the changes, and use them for patching. 

劍橋字典：
> a computer program that can show the differences between computer files


重點：
- diff 本身意思為多個事物間的不同處
- 在電腦科學是指一個程式，專門比對多個檔案的內容或者比對同一個檔案在不同版本的內容來得到差異
- diff 若作為動詞則是以第二點提出的工具來比對獲得差異，diffing 使用工具來比對獲得差異的過程或者行為



### Patch 命名緣由

- Patch 單純意思
noun
> A patch is a piece of material which you use to cover a hole in something.

verb
> If you patch something that has a hole in it, you mend it by fastening a patch over the hole. 


- 電腦科學的意思
劍橋字典：
> a small computer program that can be added to an existing program in order to make the existing program work as it should

[[@wikidataPatchComputing2022]]
> A patch is a set of changes to a computer program or its supporting data designed to update, fix, or improve it.


重點：
- patch 名詞是指一塊材料，會被縫補在特定事物上的洞上
- patch 動詞是指以一塊材料來縫補特定事物的洞之動作
- patch 在電腦科學裡上會分別是指：
	- 動詞，以特定程式碼來修正特定程式所擁有的問題
	- 名詞，負責修正特定程式所擁有的問題之特定程式碼
	- 特定程式碼實際上會是程式A修正前版本和程式A修正後版本的程式碼之差異，接著會搭配特定程式模組來以特定程式碼指示如何改變程式程式A的程式碼來修正問題
- 在這裡，會將特定程式比喻特定事物，而bug/有問題的地方則是比喻特定事物上的洞，patch則是以修正問題來比喻填補洞。


## 複習

#🧠 diff 命名緣由為何？ ->->-> `本身意思為多個事物間的不同處`

#🧠 diff 在電腦科學裡的命名緣由為何？  ->->-> `一個程式，專門比對多個檔案的內容或者比對同一個檔案在不同版本的內容來得到差異`

#🧠 diff 在電腦科學裡作為ㄉㄨ ->->-> ``

#🧠 Question :: ->->-> ``


#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

#🧠 Question :: ->->-> ``

---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@wikidataPatchComputing2022]]
[[@wikidataDiff2022]]
[[@ithomeDay04DOM]]
[[@qianduanmiVirtualDomHeDiffSuanFaTengXunYunKaiFaZheSheQuTengXunYun]]