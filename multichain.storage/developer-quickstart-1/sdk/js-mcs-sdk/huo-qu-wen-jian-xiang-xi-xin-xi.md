---
description: 获取有关特定文件的详细信息
---

# 获取文件详细信息

``

```
getFileDetails(sourceFileUploadId, dealId)
```

下面的代码示例获取上载的文件的文件详细信息。此方法获取文件的上传 ID 和文件的交易 ID。交易 ID 可以通过 getUploads 方法获取

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')
const fs = require('fs') // used to read files

// set up js-mcs-sdk
const mcs = new mcsSDK({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
})

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = ''
  const DEAL_ID = ''
   
  console.log(await mcs.getFileDetails(SOURCE_FILE_UPLOAD_ID, DEAL_ID))
}

main()
```

* **sourceFileUploadId**：文件的上传 ID
* **dealId**： 文件的 deal id

#### 返回 <a href="#fan-hui-4" id="fan-hui-4"></a>

返回来自 `/deal/detail/` API 的响应

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
      ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
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
