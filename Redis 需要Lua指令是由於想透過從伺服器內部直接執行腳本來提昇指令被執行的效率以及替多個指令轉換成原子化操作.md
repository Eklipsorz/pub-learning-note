
## 描述

[[@KuaiSuRuMenRedisHuJiaoLuaZhiLingMaJiShiYongChangJingJieShaoZiMuGeBuLuoGeMdEditor]] 所描述：

> **簡而言之：Lua指令碼帶來效能的提升**。

> -   很多應用的服務任務包含多步redis操作以及使用多個redis命令，這時你可以使用Redis結合Lua指令碼，會為你的應用帶來更好的效能。
> -   另外包含在一個Lua腳本里面的redis命令具備原子性，當你面對高併發場景下的redis資料庫操作時，可以有效避免多執行緒操作產生髒資料。

[[@RedisXueXiZhiluaJianShu]] 所描述：

> redis在2.6开始加入了lua脚本，使用lua脚本有如下好处:

> -   **减少网络开销**。复合操作需要向Redis发送多次请求，如上例，而是用脚本功能完成同样的操作只需要发送一个请求即可，减少了网络往返时延。
> -   **原子操作**。Redis会将整个脚本作为一个整体执行，中间不会被其他命令插入。换句话说在编写脚本的过程中无需担心会出现竞态条件，也就无需使用事务。事务可以完成的所有功能都可以用脚本来实现
> -   **复用**。客户端发送的脚本会永久存储在Redis中，这就意味着其他客户端（可以是其他语言开发的项目）可以复用这一脚本而不需要使用代码完成同样的逻辑

[[@redisScriptingLuaRedis]]
> Redis lets users upload and execute Lua scripts on the server. Scripts can employ programmatic control structures and use most of the [commands](https://redis.io/commands) while executing to access the database. Because scripts execute in the server, reading and writing data from scripts is very efficient.

> Redis guarantees the script's atomic execution. While executing the script, all server activities are blocked during its entire runtime. These semantics mean that all of the script's effects either have yet to happen or had already happened.

> Scripting offers several properties that can be valuable in many cases. These include:

> -   Providing locality by executing logic where data lives. Data locality reduces overall latency and saves networking resources.
> -   Blocking semantics that ensure the script's atomic execution.
> -   Enabling the composition of simple capabilities that are either missing from Redis or are too niche to a part of it.

重點：
- Redis 為什麼需要Lua指令碼? 主要原因有兩個：
	- 是透過從伺服器內部直接執行腳本來提昇指令被執行的效率，而不是伺服器和請求方還隔著網路來進行傳遞
	- 實現多個指令的原子化：透過腳本內容來定義哪些指令要被合併在一個檔案，接著執行時，Redis就直接以那檔案來執行
- 這樣會帶來以下幾個好處：
	- 本身就有的原子化特性：當Redis伺服器執行lua腳本時會保證這些腳本所定義的指令將會是以原子化來執行，具體會是當執行lua腳本時，在執行期間，伺服器所有活動將會被阻塞，直到lua腳本被執行完畢
	- 減少網路開銷：透過多個指令合併成單一指令，可使原本N個指令所產生出來的N個請求 轉換成只需要一個請求，而這個請求就是請求伺服器執行指定腳本內容
	- 重複使用：以lua程式腳本來模組化可重複使用的功能，在下一次需要同樣功能時，就載入已經定義好的lua腳本

## 複習
#🧠 Redis 為什麼需要Lua指令碼？ ->->-> `是透過從伺服器內部直接執行腳本來提昇指令被執行的效率，而不是伺服器和請求方還隔著網路來進行傳遞、實現多個指令的原子化：透過腳本內容來定義哪些指令要被合併在一個檔案，接著執行時，Redis就直接以那檔案來執行`

#🧠 Redis 鑲入Lua指令碼會有什麼好處？ ->->-> `減少網路開銷、實現原子化特性、可以定義成可重複使用的程式模組`

#🧠  Redis 鑲入Lua指令碼如何實現減少網路開銷->->-> `透過多個指令合併成單一指令，可使原本N個指令所產生出來的N個請求 轉換成只需要一個請求，而這個請求就是請求伺服器執行指定腳本內容`

#🧠 Redis 採用Lua具體如何實現原子化操作？->->-> `具體會是當執行lua腳本時，在執行期間，伺服器所有活動將會被阻塞，直到lua腳本被執行完畢`

---
Status: #🌱 
Tags:
[[Redis]] - [[Lua]]
Links:
References:
[[@redisScriptingLuaRedis]]
[[@RedisXueXiZhiluaJianShu]]
[[@KuaiSuRuMenRedisHuJiaoLuaZhiLingMaJiShiYongChangJingJieShaoZiMuGeBuLuoGeMdEditor]]

