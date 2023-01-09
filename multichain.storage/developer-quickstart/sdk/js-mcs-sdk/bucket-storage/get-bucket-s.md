---
description: Get the list of buckets
---

# Get Bucket(s)

`getBuckets()`, `getBucketList()`

These two functions are actually interchangeable, if no `bucketName` is specified, it will return the list of buckets.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let bucketInfo = await mcs.getBuckets()
  console.log(bucketInfo)
}

main()
```

### Return

```
{
  status: 'success',
  data: [
    {
      BucketUid: 'ca0...f37',
      Address: '0xb...AaB',
      MaxSize: 34359738368,
      Size: 0,
      IsFree: true,
      PaymentTx: '',
      IsActive: true,
      IsDeleted: false,
      BucketName: 'test-bucket',
      FileNumber: -2,
      ID: 244,
      CreatedAt: '2023-01-03T18:35:28Z',
      UpdatedAt: '2023-01-03T18:35:28Z',
      DeletedAt: null
    }
  ]
}
```
