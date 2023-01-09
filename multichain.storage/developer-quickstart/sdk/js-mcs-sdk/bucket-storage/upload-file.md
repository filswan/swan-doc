---
description: Upload a file to an existing bucket
---

# Upload File

`uploadToBucket(filePath, bucketUid, folderPrefix='', options={ log: false })`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const FILE_PATH = ''
  const BUCKET_UID = ''
  const FOLDER_PREFIX = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let uploadResponse = await mcs.uploadToBucket(FILE_PATH, BUCKET_UID, FOLDER_PREFIX)
  console.log(uploadResponse)
}

main()
```

### Parameters

* **filePath**: The path to the file
* **bucketUid**: The bucket uid
* **folderPrefix**: The subfolder path in the bucket ex. 'folder1/folder2'

### Return

```
{
  status: 'success',
  data: {
    file_id: <file_id>,
    file_hash: '7e...96',
    file_is_exist: false,
    ipfs_is_exist: false,
    size: 63447054,
    payload_cid: 'Qme...kMr',
    ipfs_url: 'https://ipfs.multichain.storage/ipfs/Qm...'
  }
}
```
