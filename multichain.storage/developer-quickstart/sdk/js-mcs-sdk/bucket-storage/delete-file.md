---
description: Delete a file (or folder) from an existing bucket
---

# Delete File

`deleteFile(fileId)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const FILE_ID = ''

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  let deleteResponse = await mcs.deleteFile(FILE_ID)
  console.log(deleteResponse)
}

main()
```

### Parameters

* **fileId**: The file/folder id

### Return

```
{ status: 'success' }
```
