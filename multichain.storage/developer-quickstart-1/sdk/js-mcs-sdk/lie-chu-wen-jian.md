---
description: 查看您上传的文件
---

# 列出文件

```
getUploads(walletAddress, payloadCid, fileName, orderBy, isAscend, status, isMinted, pageNumber, pageSize)
```

下面的代码示例列出用户上载的文件。该列表可以按文件名搜索，也可以进行筛选或排序。

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
  const FILE_NAME = ''
  const ORDER_BY = ''
  const IS_ASCEND = ''
  const STATUS = ''
  const IS_MINTED = ''
  const PAGE_NUMBER = 1
  const PAGE_SIZE = 10
  
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

#### 参数 <a href="#can-shu-2" id="can-shu-2"></a>

**walletAddress**：列出此帐户上传的文件（必填）

**fileName**：按此文件名筛选

**orderBy**：按文件名、文件大小或上传时间（默认）对列表进行排序

**isAscend**：y 表示升序列表，否则为降序（默认）

**status**： 待处理， 正在处理， 可退款， 已退款， 成功或其他

**isMinted**： y， n， all （默认）

**pageNumber**：页码（默认为 1）

**pageSize**：页面中的结果数（默认为 10）

只有钱包地址参数是必需的，其余的是可选的。

#### 返回 <a href="#fan-hui-3" id="fan-hui-3"></a>

返回一个数组，其中包含文件的一些详细信息。

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
