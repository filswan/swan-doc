---
description: Get Filecoin storage status of a file
---

# Get Filecoin Status for File

`getFileStatus(dealId)`

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal id of the deal. This can also be obtained by the getUploads method.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')
const fs = require('fs') // used to read files

async function main() {
  // ENTER PARAMETERS
  const DEAL_ID = 0
  
  const mcs = await mcsSDK.initialize({
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  const mintResponse = await mcs.getFileStatus(DEAL_ID)
  console.log(mintResponse)
}

main()
```

### Parameters

* **dealId**: deal id of the file

### Return

Returns the response from the `/deal/log/` API

```
{
  status: 'success',
  data: {
    offline_deal_log: [ [Object], [Object], [Object], [Object], [Object], [Object] ]
  }
}
```
