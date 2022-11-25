---
description: Get the list of buckets or information on a specific bucket
---

# Get Bucket(s)

`getBuckets()`, `getBucket(bucketName)`

These two functions are actually interchangeable, if no `bucketName` is specified, it will return the list of buckets.

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
  
  let bucketInfo = await mcs.getBucket(BUCKET_NAME)
  console.log(bucketInfo.data)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket (optional)

### Return

This is the return from the bucket list

```
{
  parent: <id>,
  objects: [
    {
      id: <bucket_id>,
      name: <bucket_name>,
      path: '/',
      pic: '',
      size: 0,
      type: 'dir',
      payload_cid: '',
      ipfs_url: '',
      pin_status: '',
      date: '2022-11-25T17:17:42Z',
      files_count: 0,
      create_date: '2022-11-25T17:17:42Z',
      update_date: '2022-11-25T17:17:42Z',
      source_enabled: false
    }
  ],
  policy: {
    id: <policy_id>,
    name: 'default',
    type: 'local',
    max_size: 32212254720,
    file_type: []
  },
  folder_cnt: 1,
  free_folder_cnt: 0,
  file_cnt: 0
}
```

This is the return from getting a specific bucket

```
{
  parent: <bucket_id>,
  objects: [],
  policy: {
    id: <policy_id>,
    name: 'default',
    type: 'local',
    max_size: 32212254720,
    file_type: []
  },
  folder_cnt: 0,
  free_folder_cnt: 0,
  file_cnt: 0
}
```
