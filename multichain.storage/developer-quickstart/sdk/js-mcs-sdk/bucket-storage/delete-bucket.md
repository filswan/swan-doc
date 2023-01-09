---
description: Delete a Bucket
---

# Delete Bucket

`deleteBucket(bucketUid)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_UID = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let deleteBucketResponse = await mcs.deleteBucket(BUCKET_UID)
}

main()
```

### Parameters

* **bucketUid**: The bucket uid

### Return

```
{ status: 'success' }
```
