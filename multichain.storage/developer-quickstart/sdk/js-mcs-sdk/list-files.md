---
description: View your uploaded files
---

# List Files

`getUploads(walletAddress, payloadCid, fileName, orderBy, isAscend, status, isMinted, pageNumber, pageSize)`

The following code example lists a user's uploaded files. The list can be searched by file name, and also be filtered or sorted.

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk') // or any of the other environments
const fs = require('fs') // used to read files

async function main() {
  // ENTER PARAMETERS
  const FILE_NAME = ''
  const ORDER_BY = ''
  const IS_ASCEND = ''
  const STATUS = ''
  const IS_MINTED = ''
  const PAGE_NUMBER = 1
  const PAGE_SIZE = 10
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.MUMBAI_RPC_URL,
  })
  
  const uploads = await mcs.getUploads(
    mcs.publicKey,
    FILE_NAME,
    ORDER_BY,
    IS_ASCEND,
    STATUS,
    IS_MINTED,
    PAGE_NUMBER,
    PAGE_SIZE,
  )
  
  console.log(uploads.data.source_file_upload)
}

main()
```

### Parameters

* **walletAddress**: lists the files uploaded by this account (required)
* **fileName**: filter by this file name
* **orderBy**: sort the list by file name, file size, or upload time (default)
* **isAscend**: y for ascending list, otherwise descend (default)
* **status**: Pending, Processing, Refundable, Refunded, Success or other
* **isMinted**: y, n, all (default)
* **pageNumber**: page number (default 1)
* **pageSize**: number of results in a page (default 10)

Only the walletAddress parameter is required, the rest are optional.

### Return

Returns an array containing some details of the file(s).

```
[
  {
    source_file_upload_id: <ID>,
    car_file_id: <ID>,
    file_name: <FILE_NAME>,
    file_size: <FILE_SIZE>,
    upload_at: <TIME>,
    duration: 525,
    ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
    pin_status: 'Pinned',
    payload_cid: <'bafy...'>,
    w_cid: <UNIQUE_CID>,
    status: 'Processing',
    deal_success: <BOOLEAN>,
    is_minted: <BOOLEAN>,
    token_id: <ID>,
    mint_address: '0x1A1e5AC88C493e0608C84c60b7bb5f04D9cF50B3',
    nft_tx_hash: <'0x...'>,
    offline_deal: [ [Object], [Object], [Object], [Object], [Object] ]
  }, ...
]
```
