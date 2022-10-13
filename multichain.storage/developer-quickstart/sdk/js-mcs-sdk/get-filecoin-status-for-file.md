---
description: Get Filecoin storage status of a file
---

# Get Filecoin Status for File

`getFileStatus(dealId)`

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal id of the deal. This can also be obtained by the getUploads method.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk') // or any of the other environments
const fs = require('fs') // used to read files

async function main() {
  // ENTER PARAMETERS
  const DEAL_ID = 0
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.MUMBAI_RPC_URL,
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
