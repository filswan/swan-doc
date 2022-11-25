---
description: Upload a file to an existing bucket
---

# Upload File to Bucket

`uploadToBucket(bucketName, fileName, filePath)`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const FILE_NAME = ''
  const FILE_PATH = ''

  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
  
  let uploadResponse = await mcs.uploadToBucket(BUCKET_NAME, FILE_NAME, FILE_PATH)
  console.log(uploadResponse)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket&#x20;
* **fileName**: The name of the file (unique)
* **filePath**: The path to the file

### Return

```
{ status: 'success' }
```
