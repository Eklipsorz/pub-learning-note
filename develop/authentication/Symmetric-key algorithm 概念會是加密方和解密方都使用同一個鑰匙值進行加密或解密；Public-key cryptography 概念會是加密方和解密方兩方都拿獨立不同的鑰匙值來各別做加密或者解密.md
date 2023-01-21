## 描述


### Symmetric-key algorithm 和 Public-key cryptography給定的鑰匙

加密方和解密方會用到的鑰匙會從：
1. 進行前事先定義
2. 在過程中傳遞一組鑰匙來配合

會這樣安排，主因為：
1. 加解密需要鑰匙值來進行
2. 加密方和解密方一開始不會有鑰匙值

### Symmetric-key algorithm

[[@DuiChengMiYaoJiaMi2022]]
> 對稱密鑰演算法（英語：Symmetric-key algorithm）又稱為對稱加密、私鑰加密、共享密鑰加密，是密碼學中的一類加密演算法。這類演算法在加密和解密時使用相同的密鑰

重點：
- 加密方和解密方都使用同一個鑰匙值進行加密/解密
- 鑰匙本身可以搭配特定算法來做加密、解密
- 適合場景：
	- 通訊雙方會事先定義好會使用相同的鑰匙，不需要在網路上另外傳遞

### Public-key cryptography
[[@GongKaiJinYaoJiaMiWeiJiBaiKeZiYouDeBaiKeQuanShu]]

> 公開金鑰密碼學（英語：Public-key cryptography）也稱非對稱式密碼學（英語：Asymmetric cryptography）是密碼學的一種演算法，它需要兩個金鑰，一個是公開密鑰，另一個是私有密鑰；公鑰用作加密，私鑰則用作解密。使用公鑰把明文加密後所得的密文，只能用相對應的私鑰才能解密並得到原本的明文，最初用來加密的公鑰不能用作解密。由於加密和解密需要兩個不同的密鑰，故被稱為非對稱加密；不同於加密和解密都使用同一個密鑰的對稱加密

> ### 加密
> 非對稱加密往往需要密碼學安全偽亂數生成器的協助來產生一對金鑰，其中一個可以隨便公開，稱為公鑰；另一個不公開，稱為私鑰，必須由使用者自行嚴格秘密保管，絕不透過任何途徑向任何人提供。
> 
> 如果任何人使用公鑰加密明文，得到的密文可以透過不安全的途徑（如網路）傳送，只有對應的私鑰持有者才可以解密得到明文；其他人即使從網路上竊取到密文及加密公鑰，也無法（在數以年計的合理時間內）解密得出明


> ### 數位簽章

> 相反，如果某一使用者使用他的私鑰加密明文，任何人都可以用該使用者的公鑰解密密文；由於私鑰只由該使用者自己持有，故可以肯定該檔案必定出自於該使用者




重點：
- 加密方和解密方兩方都拿獨立不同的鑰匙值來各別做加密/解密。
	- 加密方使用密鑰，解密方使用公鑰
	- 加密方使用公鑰，解密方使用密鑰
- Public-key cryptography 可以實現：
	- 內容加密和解密：加密方使用公鑰，解密方使用密鑰，在這裡使用公鑰加密過的任意秘文，只能用特定密鑰才能解密，一般公鑰無法解密
	- 驗證是否竄改內容的數位簽章：加密方使用密鑰，解密方使用公鑰。
- 適用場景為
	- 通訊雙方透過網路獲取鑰匙
	- 通訊雙方事先被給定鑰匙


#### 基於Public-key cryptography 的 數位簽章

[[@ShuWeiQianZhangWeiJiBaiKeZiYouDeBaiKeQuanShu]]
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/57/Digital_Signature_diagram_zh-tw.svg/1280px-Digital_Signature_diagram_zh-tw.svg.png)

重點：
- 數位簽章具體有簽名、驗證這兩個流程，簽名方和驗證方都擁有相同的hashing algorithm、相同的secret
	- 簽名方簽名：會使用hashing algorithm 、secret、特定資料內容來生成簽署值，在使用私鑰加密簽署值，添加加密後簽署值和憑證資料至原資料上
	- 驗證方驗證簽名：當接收到添加憑證的資料時，會分別使用公鑰解密出簽署值A和使用(與簽名方相同)的hashing algorithm、secret、接收到資料產生簽署值B，並比對簽署值A和簽署值B是否一樣，若一樣就沒被篡改；若不一樣就代表被篡改。
		- 不一樣的原因：資料內容篡改、解密方使用錯誤的公鑰
		- 一樣的原因：資料內容未被篡改、解密方使用正確的公鑰
		- 使用加密/解密這方式可以確保在傳遞過程讓合法驗證方來接收正確的內容，不讓非法驗證方接到正確的內容
#### public-key & private-key

![[Pasted image 20230119210755.png]]
> 非對稱加密往往需要密碼學安全偽亂數生成器的協助來產生一對金鑰，其中一個可以隨便公開，稱為公鑰；另一個不公開，稱為私鑰，必須由使用者自行嚴格秘密保管，絕不透過任何途徑向任何人提供。

重點：
- key 可以搭配特定算法來進行加解密，根據是否開放公眾或者特定對象來分成兩種：
	- public key：開放給大眾進行加解密的鑰匙值
	- private key：僅開放給特定對象進行加解密的鑰匙值
	- 通常加密方使用其中一方，另一方使用另一方就只能使用解密；

### Symmetric vs. Asymmetric

Symmetric 
> involving actions or parts that are similar or balanced in some way

Asymmetric
> with two halves, sides, or parts that are not exactly the same in shape and size

> a state where things are of equal weight or force

重點：
- symetric：涉及的事物在特定層面下是相同、類似的；涉及的事物在特定層面下是保持對等的
- asymetric：涉及的事物在特定層面下是不同的；涉及的事物在特定層面下是保持不對等

### cryptography 

> More generally, cryptography is about constructing and analyzing protocols that prevent third parties or the public from reading private messages

protocol 
>  a formal international agreement or understandingon some matter
>  
>  the set form in which data must be presented for handling by a particular computer configuration, esp in the transmission of information between different computer systems

agreement
> the situation in which people have the same opinion, or in which they approve of or accept something

重點：
- protocol：一份用來表達多數人都同意特定想法的正式合約
- agreement：表達多數都接受特定想法的情況
- cryptography：本身會是指協議，用來構建密文和解密以防止第三方或者公眾讀取私人訊息

## 複習

#🧠  protocol 命名緣由為何？ ->->-> `一份用來表達多數人都同意特定想法的正式合約`

#🧠 agreement命名緣由為何？ ->->-> `表達多數都接受特定想法的情況`

#🧠 cryptography 命名緣由 ->->-> `本身會是指協議，用來構建密文和解密以防止第三方或者公眾讀取私人訊息`

#🧠 Symmetric-key algorithm會是指什麼？->->-> `加密方和解密方都使用同一個鑰匙值進行加密/解密`
<!--SR:!2023-01-24,3,250-->

#🧠 Symmetric-key algorithm的key用途會是指什麼？ ->->-> `鑰匙本身可以搭配特定算法來做加密、解密`

#🧠 Public-key cryptography 會把密鑰分類成什麼？ ->->-> `	- public key：開放給大眾進行加解密的鑰匙值 - private key：僅開放給特定對象進行加解密的鑰匙值 - 通常加密方使用其中一方，另一方使用另一方就只能使用解密；`

#🧠 Public-key cryptography 是什麼概念？ ->->-> `加密方和解密方兩方都拿獨立不同的鑰匙值來各別做加密/解密`
<!--SR:!2023-01-24,3,250-->

#🧠 Public-key cryptography 是拿獨立不同的密鑰來各別做加密/解密，公密鑰會如何使用？ ->->-> `	- 加密方使用密鑰，解密方使用公鑰 - 加密方使用公鑰，解密方使用密鑰`

#🧠 Public-key cryptography 可以實現什麼應用 ->->-> `內容加密和解密、驗證是否竄改內容的簽署`

#🧠 Public-key cryptography 可以實現 內容加密和解密，具體概念會是？ 以及為啥？->->-> `加密方使用公鑰，解密方使用密鑰，在這裡使用公鑰加密過的任意秘文，只能用特定密鑰才能解密，一般公鑰無法解密，在這裡，只會有特定對象的密鑰才有辦法解密讀取，其他人不能讀取`

#🧠 Public-key cryptography 可以實現 驗證是否竄改內容的簽署，具體概念會是？->->-> ` 數位簽章具體有簽名、驗證這兩個流程，簽名方和驗證方都擁有相同的hashing algorithm、相同的secret。 簽名方簽名：會使用hashing algorithm 、secret、特定資料內容來生成簽署值，在使用私鑰加密簽署值，添加加密後簽署值和憑證資料至原資料上。驗證方驗證簽名：當接收到添加憑證的資料時，會分別使用公鑰解密出簽署值A和使用(與簽名方相同)的hashing algorithm、secret、接收到資料產生簽署值B，並比對簽署值A和簽署值B是否一樣，若一樣就沒被篡改；若不一樣就代表被篡改`

#🧠 數位簽章具體有哪兩個流程 ->->-> `簽名、驗證`
<!--SR:!2023-01-24,3,250-->

#🧠 數位簽章具體有簽名、驗證這兩個流程，若驗證部分會是不一樣的話，可能性會是什麼？ ->->-> `資料內容篡改、解密方使用錯誤的公鑰`

#🧠 數位簽章具體有簽名、驗證這兩個流程，若驗證部分會是不一樣的話，可能性會是資料內容篡改、解密方使用錯誤的公鑰，那這樣能確保什麼？？ ->->-> `可以更加確保簽章會是原簽發者`

#🧠 數位簽章具體有簽名、驗證這兩個流程，流程添加非對稱加解密，是要確保什麼？ ->->-> `使用加密/解密這方式可以確保在傳遞過程讓合法驗證方來接收正確的內容，不讓非法驗證方接到正確的內容`

#🧠 數位簽章具體有簽名、驗證這兩個流程，流程添加對稱加解密，會比非對稱加解密來得好嗎？ 為啥？若事先給定鑰匙或者傳遞的話->->-> `不好，原因在於使用對稱的話，勢必得透過網路傳遞鑰匙給驗證方來做驗證，但這樣不能確保只會讓合法驗證方接收到；但若事先給定的話，就免除這問題`

#🧠  Public-key cryptography 的加密/解密鑰匙通常會事先給定嗎？還是透過網路給定->->-> `通常兩者皆行`

#🧠  Public-key cryptography 的加密/解密適合的場景->->-> `- 通訊雙方透過網路獲取鑰匙- 通訊雙方事先被給定鑰匙`

#🧠 Symmetric-key algorithm 的加密/解密鑰匙通常會事先給定嗎？還是透過網路給定->->-> `通常會是事先給定`
<!--SR:!2023-01-24,3,250-->

#🧠 Symmetric-key algorithm 的加密/解密適合的場景 ->->-> `通訊雙方會事先定義好會使用相同的鑰匙，不需要在網路上另外傳遞`
<!--SR:!2023-01-24,3,250-->

#🧠 Symmetric-key algorithm 和 Public-key cryptography給定的鑰匙皆從哪獲取？ ->->-> `1. 進行前事先定義2. 在過程中傳遞一組鑰匙來配合`
<!--SR:!2023-01-24,3,250-->


#🧠 Symmetric-key algorithm 和 Public-key cryptography給定的鑰匙皆從哪獲取？1. 進行前事先定義2. 在過程中傳遞一組鑰匙來配合，為什麼會這樣安排？ ->->-> `1. 加解密需要鑰匙值來進行 2. 加密方和解密方一開始不會有鑰匙值`


---
Status: #🌱 
Tags:
[[Authentication]]
Links:
References:
[[@DuiChengMiYaoJiaMi2022]]
[[@GongKaiJinYaoJiaMiWeiJiBaiKeZiYouDeBaiKeQuanShu]]