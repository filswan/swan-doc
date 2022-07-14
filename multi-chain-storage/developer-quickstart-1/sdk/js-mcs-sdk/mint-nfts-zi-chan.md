---
description: Mint NFT 到 MCS Opensea Collection
---

# Mint NFTs资产

Mint NFT 到 MCS Opensea Collection

```
mintAsset(sourceFileUploadId, nftObject)
```

下面的代码示例将上传的文件铸造为在 Opensea 上可查看的 NFT。创建一个 NFT 对象并提供该文件的payload\_cid。NFT 对象遵循[OpenSea元数据标准](https://docs.opensea.io/docs/metadata-standards)。

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
  const SOURCE_FILE_UPLOAD_ID = 0
  const IPFS_URL = ''
  const NFT_NAME = ''

  const NFT_DESCRIPTION = '' // optional

  const nft = {
    name: NFT_NAME, // the name of your NFT
    image: IPFS_URL, // asset URI, images will render on Opensea
    external_url: IPFS_URL, // Opensea will provide a link to view the source
    description: NFT_DESCRIPTION, // description of your NFT
    attributes: [], // NFT attributes displayed on Opensea
  }

  const mintTx = await mcs.mintAsset(SOURCE_FILE_UPLOAD_ID, nft)
  console.log(mintTx)
}

main()
```



{% embed url="https://github.com/filswan/nft" %}

#### Parameters <a href="#parameters" id="parameters"></a>

**sourceFileUploadId**：上传文件的 ID

**nftObject**：遵循 Opensea Metadata Standards 的对象

* **name**：您的 NFT 的名称（必填）
* **image**：文件的 IPFS URL（必填）
* **description**： 您的 NFT 的描述
* **attributes**：您希望在 Opensea 上显示的属性对象数组

#### 返回 <a href="#fan-hui-2" id="fan-hui-2"></a>

返回来自 `/mint/info` API 的响应

```
{
  status: 'success',
  data: {
    id: <ID>,
    source_file_upload_id: <ID>,
    nft_tx_hash: <'0x...'>,
    mint_address: '0x1A1e5AC88C493e0608C84c60b7bb5f04D9cF50B3',
    token_id: '<ID>',
    create_at: <TIME>,
    update_at: <TIME>
  }
}
```
