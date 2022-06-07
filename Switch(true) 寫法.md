```
switch (true) {
	case (!isExistInCache && !isExistInDB):
		// case 1: There is nothing on cache and DB
		// do nothing
		break

	case (!isExistInCache && isExistInDB):
		// case 2: Except for cache, there is a cart data on DB
		await CartPreprocessor.syncCartFromDBtoCache(req)
		break

	case (isExistInCache && !isExistInDB):
		// case 3: Except for DB, there is a cart data on cache
		await CartPreprocessor.syncCartFromCachetoDB(req)
		break

	case (isExistInCache && isExistInDB):
		// case 4: There is a cart data on cache and DB
		await CartPreprocessor.syncCartToDBAndCache(req)
		break
}
```