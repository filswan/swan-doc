---
description: Create a subfolder
---

# Create Folder

`createFolder(bucketUid, folderName, folderPrefix)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_UID = ''
  const FOLDER_NAME = ''
  const FOLDER_PREFIX = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let folderResponse = await mcs.createFolder(BUCKET_UID, FOLDER_NAME, FOLDER_PREFIX)
  console.log(folderResponse)
}

main()
```

### Parameters

* **fileId**: The file/folder id

### Return

```
{ status: 'success', data: <folder_name> }
```
