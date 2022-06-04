
## 描述

重點：
- UUID 全名為
- 本身重複機率近為0，這樣能捨棄檢查重複的成本
- cartID採用


引用[[@ModelBasicsSequelize]]所描述

migration file 主要設定為：
	- 設定id為UUID
	- 其id不能為空、要用作主鍵
	- 預設值會自己產生UUIDv4的UUID
```
'use strict'

module.exports = {

	async up(queryInterface, Sequelize) {
		await queryInterface.createTable('carts', {
			id: {
				allowNull: false,
				primaryKey: true,
				type: Sequelize.UUID,
				defaultValue: Sequelize.UUIDV4
			},
			user_id: {
				type: Sequelize.INTEGER
			},
			.
			.
			.

		})
	},

	async down(queryInterface, Sequelize) {
		await queryInterface.dropTable('carts')
	}	
}
```



---
Status: #📥 
Tags:
[[Sequelize]] - [[MySQL]]
Links:
References:
[[@ModelBasicsSequelize]]
[[@wikidataTongYongWeiYiShiBieMa2022]]
