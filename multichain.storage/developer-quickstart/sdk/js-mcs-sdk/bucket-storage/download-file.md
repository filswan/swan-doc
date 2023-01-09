---
description: Download a File from a bucket
---

# Download File

`downloadFile(fileId, outputDirectory)`

Downloads an uploaded file in a bucket, to the desired `outputDirectory`

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const FILE_ID = ''
  const OUTPUT_DIRECTORY = '.'

  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  await mcs.downloadFile(FILE_ID, OUTPUT_DIRECTORY)
}

main()
```

### Parameters

* **bucketName**: The name of the bucket&#x20;
* **fileName**: The name of the file (unique)
* **outputDirectory**: output directory for the file (optional, defaults to current directory)
