---
description: Mint NFT to MCS Opensea Collection
---

# Mint Assets as NFTs

`mintAsset(sourceFileUploadId, nftObject)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).&#x20;

```
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
```



{% embed url="https://github.com/filswan/nft" %}

### Parameters

* **sourceFileUploadId**: upload Id of the file
* **nftObject**: object following Opensea Metadata Standards
  * **name**: name of your NFT (required)
  * **image**: IPFS URL of your file (required)
  * **description**: description of your NFT
  * **attributes**: array of attribute objects you wish to show on Opensea

### Return

Returns the response from the `/mint/info` API
