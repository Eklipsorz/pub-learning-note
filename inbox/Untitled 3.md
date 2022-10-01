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


### Diff 命名緣由

diff 單純意思：
> short for difference 

diff 在電腦科學的意思：
[[@wikidataDiff2022]]
> In computing, the utility diff is a data comparison tool that computes and displays the differences between the contents of files

> Typically, _diff_ is used to show the changes between two versions of the same file

> The utility displays the changes in one of several standard formats, such that both humans or computers can parse the changes, and use them for patching. 


> a computer program that can show the differences between computer files


### Patch 命名緣由



## 複習


---
Status: #🌱 #📓 
Tags:
[[React]]
Links:
References:
[[@wikidataDiff2022]]
[[@ithomeDay04DOM]]
[[@qianduanmiVirtualDomHeDiffSuanFaTengXunYunKaiFaZheSheQuTengXunYun]]