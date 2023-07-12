
原本為
```
const { SyncDBKit } = require('../config/app').utility
```

由於config檔案內會與調用該檔案的檔案內容起衝突，所以一律採用config
```
const config = require('../config/app').utility.SyncDBKit
```