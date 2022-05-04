# Mint Assets as NFTs

`mintAsset(payloadCid, nftObject)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).&#x20;

```
const PAYLOAD_CID = ''
const IPFS_URL = ''
 
const nft = {
  name: 'NFT NAME', // the name of your NFT
  image: IPFS_URL, // asset URI, images will render on Opensea
  description: 'NFT DESCRIPTION', // description of your NFT
  attributes: [], // NFT attributes displayed on Opensea
}
 
const mintTx = await client.mintAsset(PAYLOAD_CID, nft)
console.log(mintTx)
```

### Parameters

* **payloadCid**: payload cid of the file
* **nftObject**: object following Opensea Metadata Standards
  * **name**: name of your NFT (required)
  * **image**: IPFS URL of your file (required)
  * **description**: description of your NFT
  * **attributes**: array of attribute objects you wish to show on Opensea

### Return

Returns the response from the `/mint/info` API
