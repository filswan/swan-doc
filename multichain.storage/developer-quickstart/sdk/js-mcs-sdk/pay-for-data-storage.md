---
description: Pay for storage on MCS
---

# Pay for data storage

`makePayment(wCid, minAmount, fileSize)`

After a file is uploaded, the file can be paid for by its payload cid. The method takes the source file upload id as the first parameter and the minimum amount as the second.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = ''
  const MIN_AMOUNT = ''
  const FILE_SIZE = ''
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
   
  const tx = await mcs.makePayment(SOURCE_FILE_UPLOAD_ID, MIN_AMOUNT, FILE_SIZE)
  console.log(tx.transactionHash)
}

main()
```

### Parameters

* **sourceFileUploadId**: unique upload id of the file
* **minAmount**: minimum amount to pay for the file (in USDC). String value to avoid Big Number precision errors. If minAmount is set to empty string or '0', it will default to calculate and use the average storage price
* **fileSize**: the size of the file

### Return

Returns a web3.js receipt object. In the example above, only the transaction hash from this object is printed.
