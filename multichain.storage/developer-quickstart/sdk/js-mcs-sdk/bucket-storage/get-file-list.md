---
description: Get list of files in a bucket
---

# Get File List

`getFileList(bucketUid, params), getFiles(bucketUid, params)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_UID = ''
  const PARAMS = {
    prefix: '',
    limit: 10,
    offset: 0
  } 

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let fileList = await mcs.getFileList(BUCKET_UID, PARAMS)
  console.log(fileList)
}

main()
```

### Parameters

* **bucketUid**: The bucket uid
* **params**
  * **prefix:** the folder prefix if you want the list of files in a subfolder
  * **limit:** number of returned files
  * **offset:** page number&#x20;

### Return

```
{
  FileList: [
    {
      Name: <bucket_name>,
      Address: '0xb...AaB',
      Prefix: '',
      BucketUid: 'ca0...f37',
      FileHash: '',
      Size: 0,
      PayloadCid: '',
      IpfsUrl: '',
      PinStatus: '',
      IsDeleted: false,
      IsFolder: true,
      ID: <bucket_id>,
      CreatedAt: '2023-01-04T16:16:27Z',
      UpdatedAt: '2023-01-04T16:16:27Z',
      DeletedAt: null
    }
  ],
  Count: 1
}
```
