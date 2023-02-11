---
description: Mint NFT to MCS Opensea Collection
---

# Mint Assets as NFTs

`mintAsset(sourceFileUploadId, nftObject)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).&#x20;

```
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = 0
  const IPFS_URL = ''
  const NFT_NAME = ''

  const NFT_DESCRIPTION = '' // optional
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })

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

### Parameters

* **sourceFileUploadId**: upload Id of the file
* **nftObject**: object following Opensea Metadata Standards
  * **name**: name of your NFT (required)
  * **image**: IPFS URL of your file (required)
  * **description**: description of your NFT
  * **external\_url**: viewable link on Opensea UI
  * **attributes**: array of attribute objects you wish to show on Opensea

### Return

Returns the response from the `/mint/info` API

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