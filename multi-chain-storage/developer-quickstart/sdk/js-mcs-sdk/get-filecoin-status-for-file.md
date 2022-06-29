---
description: Get Filecoin storage status of a file
---

# Get Filecoin Status for File

`getFileStatus(dealId)`

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal id of the deal. This can also be obtained by the getUploads method.

```
require('dotenv').config()
const { mcsSdk } = require('js-mcs-sdk')
const fs = require('fs') // used to read files

// set up js-mcs-sdk
const mcs = new mcsSdk({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  // ENTER PARAMETERS
  const DEAL_ID = 0
  
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
