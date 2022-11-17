## 描述




### history.push & replace的隱患

1. 若每一次對stack的最上面元素做push或replace，會使react執行一次unmount 和 一次mount，而不是針對差異來切換。
2. 延續第一項，即使是一直push相同頁面的網址，也是會執行unmount 和 mount


## 複習
#🧠 react-router-dom：history.push & replace的隱患是什麼？(說到相同頁面) ->->-> `若每一次對stack的最上面元素做push或replace，會使react執行一次unmount 和 一次mount，而不是針對差異來切換，延續第一項，即使是一直push相同頁面的網址，也是會執行unmount 和 mount`

#🧠 react-router-dom：history.push & replace的隱患是什麼？->->-> `若每一次對stack的最上面元素做push或replace，會使react執行一次unmount 和 一次mount，而不是針對差異來切換，延續第一項，即使是一直push相同頁面的網址，也是會執行unmount 和 mount`




#🧠 react-router-dom：history.push & replace的隱患是若每一次對stack的最上面元素做push或replace，會使react執行一次unmount 和 一次mount，而不是針對差異來切換。那如果是相同頁面的網址呢 ->->-> `延續第一項，即使是一直push相同頁面的網址，也是會執行unmount 和 mount`

---
Status:  #🌱 
Tags:
[[React]]
Links:
[[react-router-practice：使用useHistory來實現programmatic navigation，具體會是操縱瀏覽器的瀏覽紀錄來進行]]
References: