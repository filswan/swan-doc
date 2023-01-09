---
description: Create a Bucket
---

# Create Bucket

`createBucket(bucketName)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let createBucketResponse = await mcs.createBucket(BUCKET_NAME)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket&#x20;

### Return

```
{ status: 'success', data: <bucket_uid> }
```
