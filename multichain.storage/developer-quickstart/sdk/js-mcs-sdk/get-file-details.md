---
description: Get Details about a specific file
---

# Get File Details

`getFileDetails(sourceFileUploadId, dealId)`

The following code example gets the file details of an uploaded file. This method takes the upload id of the file, and the deal id of the file. The deal id can be obtained by the getUploads method

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk') 
const fs = require('fs') // used to read files

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = ''
  const DEAL_ID = ''
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    rpcUrl: process.env.RPC_URL,
  })
   
  console.log(await mcs.getFileDetails(SOURCE_FILE_UPLOAD_ID, DEAL_ID))
}

main()
```

### Parameters

* **sourceFileUploadId**: upload id of the file
* **dealId**: deal id of the file

### Return

Returns the response from the `/deal/detail/` API

```
{
  status: 'success',
  data: {
    dao_signature: [ [Object], [Object], [Object], [Object] ],
    dao_threshold: 2,
    source_file_upload_deal: {
      deal_id: <ID>,
      deal_cid: '',
      message_cid: <'bafy...'>,
      height: <NUMBER>,
      piece_cid: <'...'>,
      verified_deal: <BOOLEAN>,
      storage_price_per_epoch: 0,
      signature: '',
      signature_type: '',
      created_at: <TIME>,
      piece_size_format: null,
      start_height: <NUMBER>,
      end_height: <NUMBER>,
      client: <'f...'>,
      client_collateral_format: '000000000000000000',
      provider: <'f...'>,
      provider_tag: '',
      verified_provider: 0,
      provider_collateral_format: '000000000000000000',
      status: 0,
      network_name: 'filecoin_mainnet',
      storage_price: 0,
      ipfs_url: <'https://ipfs.multichain.storage/ipfs/Qm...'>,
      file_name: <FILE_NAME>,
      w_cid: <UNIQUE_CID>,
      car_file_payload_cid: <'bafy...'>,
      locked_at: <TIME>,
      locked_fee: <AMOUNT>,
      unlocked: <BOOLEAN>
    }
  }
}
```
