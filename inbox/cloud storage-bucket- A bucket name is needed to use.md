


```
// Imports the Google Cloud client library
const {Storage} = require('@google-cloud/storage');
// For more information on ways to initialize Storage, please see
// https://googleapis.dev/nodejs/storage/latest/Storage.html
// Creates a client using Application Default Credentialsconst storage = new Storage();// Creates a client from a Google service account key// const storage = new Storage({keyFilename: 'key.json'});/** * TODO(developer): Uncomment these variables before running the sample. */// The ID of your GCS bucket// const bucketName = 'your-unique-bucket-name';async function createBucket() {  // Creates the new bucket  await storage.createBucket(bucketName);  console.log(`Bucket ${bucketName} created.`);}
createBucket().catch(console.error);
```

https://cloud.google.com/storage/docs/reference/libraries#client-libraries-usage-nodejs
## 描述
引用[[@googlecloudGcloudTopicGcloudignore]]所描述：

> Several commands in `[gcloud](https://cloud.google.com/sdk/gcloud/reference)` involve uploading the contents of a directory to Google Cloud to host or build. In many cases, you will not want to upload certain files (i.e., "ignore" them).

> If there is a file called `.gcloudignore` `in the top-level directory to upload`, the files that it specifies (see "SYNTAX") will be ignored.

gcloud內的部分指令會涉及**將目前目錄的內容上傳至主機或者build程序**，
```
gcloud app deploy 
```

而當中若不想把部分檔案也一併上傳就設定檔案位置至本地專案下的.gcloudignore，到時gcloud當要上傳時就會優先讀取該檔案來決定忽略哪些檔案來上傳

### 由.gcloudignore帶來的問題


.gcloudignore
```
# This file specifies files that are *not* uploaded to Google Cloud
# using gcloud. It follows the same syntax as .gitignore, with the addition of
# "#!include" directives (which insert the entries of the given .gitignore-style
# file at that point).
```


疑似gcloudignore出的問題，當時有設定
```
temp/

config/credentials/*
config/ssl/db/client-*
config/ssl/db/server-*
.env 
```

而問題剛好都是從.env和ssl目錄下出現的問題：
- 找不到對應Node.js 執行下的環境變數
- 找不到對應的ssl目錄下的檔案

若簡化成以下，就會解決
```
temp/
```

### 實驗由.gcloudignore帶來的問題
流程：
- 先在.gcloudignore設定，接著觸發部署，部署期間會建立.env，並於最後步驟上傳，但在這裡會省略.env檔案
```
.env
```

- 於app.js寫入console.log來調查
```
console.log(process.env)
```

結果是不存在我所預定設定的變數，或者說部署期間建立的.env沒被上傳至production環境-app engine
```
2022-05-24 17:12:44 default[20220524t165718]  {
2022-05-24 17:12:44 default[20220524t165718]    S2A_ACCESS_TOKEN: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_MEMORY_MB: ''skip',
2022-05-24 17:12:44 default[20220524t165718]    NO_UPDATE_NOTIFIER: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_INSTANCE: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    HOME: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    PORT: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    NODE_OPTIONS: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_SERVICE: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    PATH: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_DEPLOYMENT_ID: 'skip'
2022-05-24 17:12:44 default[20220524t165718]    DEBIAN_FRONTEND: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GOOGLE_CLOUD_PROJECT: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_ENV: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    PWD: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_APPLICATION: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_RUNTIME: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    GAE_VERSION: 'skip',
2022-05-24 17:12:44 default[20220524t165718]    NODE_ENV: 'skip'
2022-05-24 17:12:44 default[20220524t165718]  }
```

而這使得部分功能因為沒載入正確的環境變數而失敗。

若將第一個步驟還原的話，

---
Status: #🌱 
Tags:
[[GCP]] 
Links:
References:
[[@googlecloudGcloudTopicGcloudignore]]