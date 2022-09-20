---
description: Pay for storage on MCS
---

# Pay for data storage

`makePayment(wCid, minAmount, fileSize)`

After a file is uploaded, the file can be paid for by its payload cid. The method takes the w\_payload cid as the first parameter and the minimum amount as the second.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

// set up js-mcs-sdk
const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  // ENTER PARAMETERS
  const W_CID = ''
  const MIN_AMOUNT = '1'
  const FILE_SIZE = ''
   
  const tx = await mcs.makePayment(W_CID, MIN_AMOUNT, FILE_SIZE)
  console.log(tx.transactionHash)
}

main()
```

### Parameters

* **wCid**: unique payload cid of the file
* **minAmount**: minimum amount to pay for the file (in USDC). String value to avoid Big Number precision errors. If minAmount is set to empty string or '0', it will default to calculate and use the average storage price
* **fileSize**: the size of the file

### Return

Returns a web3.js receipt object. In the example above, only the transaction hash from this object is printed.
