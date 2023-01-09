---
description: Get file details
---

# Get File Info

`getFileInfo(fileId)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const FILE_ID = ''

  const mcs = await mcsSDK.initialize({
    apiKey: process.env.API_KEY,
    accessToken: process.env.ACCESS_TOKEN,
  })
  
  let fileInfo = await mcs.getFileInfo(FILE_ID)
  console.log(fileInfo)
}

main()
```

### Parameters

* **fileId**: The file id

### Return

```
{
  status: 'success',
  data: {
    Name: <file_name>,
    Address: '0xb...AaB',
    Prefix: '',
    BucketUid: 'ca0...f37',
    FileHash: '7ec...996',
    Size: 63447054,
    PayloadCid: 'Qm...',
    IpfsUrl: 'https://ipfs.multichain.storage/ipfs/Qm...',
    PinStatus: 'Pinned',
    IsDeleted: false,
    IsFolder: false,
    ID: <file_id>,
    CreatedAt: '2023-01-04T16:25:24Z',
    UpdatedAt: '2023-01-04T16:25:24Z',
    DeletedAt: null
  }
}
```
