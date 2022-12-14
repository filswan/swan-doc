---
description: Delete buckets, files, or both!
---

# Delete Items

`deleteBucket(bucketId)`, `deleteFileFromBucket(fileId)`

These functions are aliases for `deleteItems(buckets, items)`, for example, calling `deleteBucket(bucketId)` will call `deleteItems(bucketId, [])`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_ID = ['']
  const FILE_ID = ['']

  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
  
  // let deleteBucketResponse = await mcs.deleteBucket(BUCKET_ID)
  // let deleteFileResponse = await mcs.deleteFileFromBucket(FILE_ID)
  let deleteResponse = await mcs.deleteItems(BUCKET_ID, FILE_ID)
  console.log(deleteResponse)
}

main()
```

### Parameters

* **bucketId**: The ID of the bucket (can be found using `getBuckets()`
* **fileId**: The id of the file

`bucketId` and `fileId` can be singular, or an array of IDs

### Return

```
{ status: 'success' }
```
