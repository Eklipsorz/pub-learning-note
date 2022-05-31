

cartId

引用[[@wikidataTongYongWeiYiShiBieMa2022]]所描述
> 通用唯一辨識碼是用於電腦體系中以辨識資訊的一個128位元識別碼。 根據標準方法生成，不依賴中央機構的註冊和分配，UUID具有唯一性，這與其他大多數編號方案不同。重複UUID碼概率接近零，可以忽略不計。

重點：
- UUID本身重複機率近為0，這樣能捨棄檢查重複的成本
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


引用[[@ModelBasicsSequelize]]所描述
> For UUIDs, use `DataTypes.UUID`. It becomes the `UUID` data type for PostgreSQL and SQLite, and `CHAR(36)` for MySQL. Sequelize can generate UUIDs automatically for these fields, simply use `DataTypes.UUIDV1` or `DataTypes.UUIDV4` as the default val

重點：
- 實際上執行migration file後，UUID會在MySQL對應成char(36)


---
Status: #📥 
Tags:
[[Sequelize]] - [[MySQL]]
Links:
References:
[[@ModelBasicsSequelize]]
[[@wikidataTongYongWeiYiShiBieMa2022]]
