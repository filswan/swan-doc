---
description: Download a File from a bucket
---

# Download File

`downloadFile(bucketName, fileName, outputDirectory)`

Downloads an uploaded file in a bucket, to the desired `outputDirectory`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const BUCKET_NAME = ''
  const FILE_NAME = ''
  const OUTPUT_DIRECTORY = '.'

  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
  
  await mcs.downloadFile(BUCKET_NAME, FILE_NAME, OUTPUT_DIRECTORY)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket&#x20;
* **fileName**: The name of the file (unique)
* **outputDirectory**: output directory for the file (optional, defaults to current directory)
