


```
// Imports the Google Cloud client library
const {Storage} = require('@google-cloud/storage');
// For more information on ways to initialize Storage, please see
// https://googleapis.dev/nodejs/storage/latest/Storage.html
// Creates a client using Application Default Credentialsconst storage = new Storage();// Creates a client from a Google service account key// const storage = new Storage({keyFilename: 'key.json'});/** * TODO(developer): Uncomment these variables before running the sample. */// The ID of your GCS bucket// const bucketName = 'your-unique-bucket-name';async function createBucket() {  // Creates the new bucket  await storage.createBucket(bucketName);  console.log(`Bucket ${bucketName} created.`);}
createBucket().catch(console.error);
```

https://cloud.google.com/storage/docs/reference/libraries#client-libraries-usage-nodejs



temp/
若這些
config/credentials/*
config/ssl/db/client-*
config/ssl/db/server-*
.env 
放入.gcloudignore


會省略掉
config/ssl/db/client-*
config/ssl/db/server-*
.env 