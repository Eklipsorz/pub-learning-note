問題：什麼是 Lock (鎖定) ？  
答案：Lock 的主要目的是避免資料發生錯誤，把不應該進行動作的指令排除在外，並讓應該進行動作的指令能夠順利完成。  
  
問題：什麼是Table Lock (表單鎖定) ？ 什麼是Row Lock (紀錄鎖定)？  
答案：表單鎖定就是將整個資料表鎖定，讓其他連線無法讀取及異動，直到資料處理完畢為止。紀錄鎖定就是將指定的紀錄鎖定，讓其他連線無法讀取及異動，直到資料處理完畢為止。  
  
問題：InnoDB與MyISAM的鎖定有何差別？  
答案：MyISAM 沒有交易功能 (Transaction)，若要避免多個連線交互執行 SQL 指令，造成資料錯亂，只好使用鎖定資料表 (Table Lock) 的方式，InnoDB則可以使用Table Lock 與Row Lock。  
  
問題：MySQL不同版本的鎖定有何差別？  
答案：MySQL不同版本的鎖定原理一樣，只是語法上有些差異。


https://www.mysql.tw/2018/06/mysql-lock-table-lockrow-lock.html
