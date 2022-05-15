sequelize.literal ＝> 將mysql 語法執行一遍並轉換成字串

  

2.48 sequelize.literal() - 字面量对象

literal(val) -> Sequelize.literal

创建一个字面量对象，该值不会转义

  

利用MYSQL語法來構建出一個欄位名稱

  

The EXISTS operator is used to test for the existence of any record in a subquery.

  

sequelize.literal('(SELECT COUNT(*) FROM Replies WHERE Replies.UserId = User.id)')

  

Creates an object representing a literal, i.e. something that will not be escaped.

  

  

  

  

  

測試inner join 和 outer join 的結果

  

exports = module.exports = tweetController

  

A->B 

=> JSON_EXTRACT （將A包含的B內容取出來)

  

用法如下：json_doc 為json檔案或者欄位所構成的集合，path則是該檔案內容或者前者所有欄位的其中一個欄位

JSON_EXTRACT(**_json_doc_**, **_path_**[, **_path_**] ...)

  

更名：

Model.findAll({

  attributes: ['foo', ['bar', 'baz'], 'qux']

})

SELECT foo, bar AS baz, qux FROM ...

  

  

-   the arrow operator: -> returns type JSON or JSONB
-   the double arrow operator: ->> returns type text

  

  

  

the first is the name of the attribute in the DB (or some kind of expression such as Sequelize.literal, Sequelize.fn and so on), and the second is the name you want the attribute to have in the returned instance

     const products = await Product.findAll({

        attributes: ['id', ['name', 'firstName']],

        raw: true

      })
	  
	  
---
Status: #📥 
Tags:
[[JavaScript]] - [[Sequelize]] - [[MySQL]]
Links:
References: