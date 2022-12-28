## 描述


### URI的Path、Query、Fragment大小寫細節

[[@wangWangZhiURLYingWenDaXiaoXieShiFouYouChaiBie2015]]

> 在網域名稱與連接埠之後，接著就是網頁的路徑。

[![mdn-url-path](https://blog.gtwang.org/wp-content/uploads/2015/11/mdn-url-path.png)](https://blog.gtwang.org/wp-content/uploads/2015/11/mdn-url-path.png)
> 這個部分的英文字母大小寫會因為伺服器的作業系統而有不同，以 Windows 的伺服器而言是不分大小寫的，但是 UNIX/Linux 系統則會區分大小寫，位於一般的使用者而言要判斷是否可以更改大小寫並不容易，建議是不要任意更改這個部分的英文大小寫。


重點：
- 雖然理論上URI的Path、Fragmenet、Query String是會以區分大小寫來解析，但仍有一些大小寫問題：
	- 應用程式伺服器會因爲作業系統和負責執行server程式的關係，會有區分大小寫和不會區分大小寫，舉例：
		- Window 伺服器 會不分大小寫
		- UNIX/Linux 系統 會區分大小寫



## 複習
#🧠 雖然理論上URI的Path、Fragmenet、Query String是會以區分大小寫來解析，但實質上會有的問題是->->-> `仍以應用程式伺服器會因爲作業系統和負責執行server程式的關係來決定是否區分大小寫`
<!--SR:!2023-02-10,50,250-->

#🧠 雖然理論上URI的Path、Fragmenet、Query String是會以區分大小寫來解析，但仍以應用程式伺服器會因爲作業系統和負責執行server程式的關係來決定是否區分大小寫，舉例來說 ->->-> `	- Window 伺服器 會不分大小寫 - UNIX/Linux 系統 會區分大小寫`
<!--SR:!2023-02-26,60,250-->


---
Status: #🌱 
Tags:
[[Rendering]]
Links:
[[URI 包含了Scheme、Host、Port、Path、Query、Fragment。其中沒分大小寫的會是Scheme和Host，有分大小寫的會是Path、Query、Fragment]]
References:[[@wangWangZhiURLYingWenDaXiaoXieShiFouYouChaiBie2015]]