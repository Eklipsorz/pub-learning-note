



```
class Collection extends Model {}  
Collection.init({  
	uid: {  
		type: DataTypes.INTEGER, 
		
		primaryKey: true,  
		autoIncrement: true 
	}  
}, { sequelize });  
  
class Collection extends Model {}  
	Collection.init({  
		uuid: {  
		type: DataTypes.UUID,  
		primaryKey: true  
		}  
	}, { sequelize });
```