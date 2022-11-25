---
description: Create a Metaspace Bucket
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
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
  
  let createBucketResponse = await mcs.createBucket(BUCKET_NAME)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket&#x20;

### Return

```
{ status: 'success' }
```
