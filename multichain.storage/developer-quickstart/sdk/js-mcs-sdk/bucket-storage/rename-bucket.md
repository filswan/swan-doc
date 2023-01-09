---
description: Rename a Bucket
---

# Rename Bucket

`renameBucket(bucketUid, bucketName)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_UID = ''
  const BUCKET_NAME = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let renameResponse = await mcs.renameBucket(BUCKET_UID, BUCKET_NAME)
}

main()
```

### Parameters

* **bucketUid:** The bucket uid
* **bucketName**: The name of the bucket&#x20;

### Return

```
{ status: 'success', data: 'rename success' }
```
