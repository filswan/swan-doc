---
description: Guide to multichain.storage's onchain storage
---

# Onchain Storage

Onchain storage allows users to upload files to the IPFS server and backup into the Filecoin network.

### Setup Web3

First, set up web3 for the SDK. This can be done by including the private key and RPC URL when initializing the SDK

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const mcs = await mcsSDK.initialize({
    rpcUrl: process.env.RPC_URL,
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
}

main()
```

Alternatively, if your SDK is already initialized, you can call the `setupWeb3` function.

```javascript
await mcs.setupWeb3(process.env.PRIVATE_KEY, process.env.RPC_URL)
```

### Upload Files

Upload file(s) to MCS using the MCS SDK

`upload(filePath, options={duration:525, fileType:0})`

You can use the upload function to upload a file to the Swan IPFS gateway.

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const FILE_PATH = ''

  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  //optional, showing default options
  const OPTIONS = {
    duration: 525, // the number of days to store the file on the Filecoin network.
    fileType: 0, // set to 1 for nft metadata files. type 1 files will not show on the UI.
  }
  
  const uploadResponses = await mcs.upload(FILE_PATH, OPTIONS)
  console.log(uploadResponses)
}

main()jav
```

#### Parameters

* **filePath:** the file path
* **options**: an optional object can also be passed to specify certain parameters:
  * **duration**: Number of days to store your file on the Filecoin network. (default 525)
  * **fileType**: Files of type one will be hidden from the upload list and the UI. NFT metadata files are type 1. (default 0)

#### Return

This function returns an array of the upload API responses.

```javascript
{
  status: 'success',
  data: {
    source_file_upload_id: <ID>,
    payload_cid: <'Qm...'>,
    ipfs_url: <'https://ipfs.multichain.storage/ipfs/Qm...'>,
    file_size: <FILE_SIZE>,
    w_cid: <UNIQUE_CID>
    status: <PAYMENT_STATUS>
  }
}
```

### Pay for data storage

Pay for storage on MCS

`makePayment(sourceFileUploadId, fileSize)`

After a file is uploaded, the file can be paid for by its source file upload id. The amount paid is estimated using the file size

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = ''
  const FILE_SIZE = ''
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
   
  const tx = await mcs.makePayment(SOURCE_FILE_UPLOAD_ID, FILE_SIZE)
  console.log(tx.transactionHash)
}

main()
```

#### Parameters

* **sourceFileUploadId**: unique upload id of the file
* **fileSize**: the size of the file

#### Return

Returns a web3.js receipt object. In the example above, only the transaction hash from this object is printed.

### Create NFT Collection

`createCollection(collectionMetadata)`

To create a new NFT Collection, you will need to provide some information about the collection, following the Opensea metadata standards.

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const COLLECTION_DATA = {
    name: '',
    description: '',
    image: '',
    external_link: '',
    seller_fee_basis_points: '',
    fee_recipient: ''
  }
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
   
  const collection = await mcs.createCollection(COLLECTION_DATA)
}

main()
```

#### Parameters

* **sourceFileUploadId**: unique upload id of the file
* **fileSize**: the size of the file

#### Return

```javascript
{
  name: 'test collection10',
  image: 'https://ipfs.multichain.storage/ipfs/Qm...',
  tx_hash: '0x...ed',
  address: '0x...29'
}
```

### List NFT Collections

`getCollections()`

List all your created NFT collections

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
   
  const collections = await mcs.getCollections()
  console.log(collections)
}

main()
```

#### Return

```javascript
{
  status: 'success',
  data: [
    {
      id: 7,
      address: '0x511765576a051a2ce002e70fc73d71d787d3378e',
      wallet_id: null,
      name: 'Swan NFT Collection',
      description: null,
      image_url: 'https://calibration-ipfs.filswan.com/ipfs/QmXK2TecdDiAEWEm9aERwQ4f6vfaQWrRReQj1k6km3dK77?filename=SwanLogo.jpeg',
      external_link: null,
      seller_fee: null,
      wallet_id_recipient: null,
      tx_hash: null,
      create_at: 1675178532,
      update_at: 1675178532,
      wallet_recipient: '',
      is_default: true
    },
    ...
  ]
}
```

### Mint Assets as NFTs

Mint NFT to MCS Opensea Collection

`mintAsset(sourceFileUploadId, nftObject, collectionAddress=undefined, receipient=<your_address>, quantity=1)`

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the source file upload id of the file. The NFT object follows the [Opensea metadata standards](https://docs.opensea.io/docs/metadata-standards).

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')

async function main() {
  // ENTER PARAMETERS
  const SOURCE_FILE_UPLOAD_ID = 0
  const NFT = {
    name: '',
    description: '',
    image: ''
  }
  collection_address = undefined

  const NFT_DESCRIPTION = '' // optional
  
  const mcs = await mcsSDK.initialize({
    privateKey: process.env.PRIVATE_KEY,
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })

  const mintTx = await mcs.mintAsset(SOURCE_FILE_UPLOAD_ID, nft, collection_address)
  console.log(mintTx)
}

main()
```

#### Parameters

* **sourceFileUploadId**: upload Id of the file
* **nftObject**: object following Opensea Metadata Standards
  * **name**: name of your NFT (required)
  * **image**: IPFS URL of your file (required)
  * **description**: description of your NFT
  * **external\_url**: viewable link on Opensea UI
  * **attributes**: array of attribute objects you wish to show on Opensea
* **collectionAddress:** collection address to mint to
* **recipient:** who will receive the NFT
* **quanity:** how many NFT to mint, (ERC-1155) default is 1.

#### Return

Returns the response from the `/mint/info` API

```javascript
{
  status: 'success',
  data: {
    id: 1962,
    source_file_upload_id: 151305,
    nft_tx_hash: '0xab655f394f6f07bc292015fa094e4de536c8059b48cc2c8743644103245805b8',
    mint_address: '0x511765576a051a2ce002e70fc73d71d787d3378e',
    nft_collection_id: 7,
    token_id: 147,
    name: 'test NFT',
    description: '',
    create_at: 1677269767,
    update_at: 1677269767
  }
}
```

### List Files

View your uploaded files

`getUploads(walletAddress, payloadCid, fileName, orderBy, isAscend, status, isMinted, pageNumber, pageSize)`

The following code example lists a user's uploaded files. The list can be searched by file name, and also be filtered or sorted.

```javascript
require('dotenv').config()
const { mcsSDK } = require('js-mcs-sdk')
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
    accessToken: process.env.ACCESS_TOKEN,
    apiKey: process.env.API_KEY,
  })
  
  const uploads = await mcs.getUploads({
    address: mcs.publicKey,
    name: FILE_NAME,
    orderBy: ORDER_BY,
    isAscend: IS_ASCEND,
    status: STATUS,
    isMinted: IS_MINTED,
    pageNumber: PAGE_NUMBER,
    pageSize: PAGE_SIZE,
  })
  
  console.log(uploads.data.source_file_upload)
}

main()
```

#### Parameters

* **walletAddress**: lists the files uploaded by this account (required)
* **fileName**: filter by this file name
* **orderBy**: sort the list by file name, file size, or upload time (default)
* **isAscend**: y for ascending list, otherwise descend (default)
* **status**: Pending, Processing, Refundable, Refunded, Success or other
* **isMinted**: y, n, all (default)
* **pageNumber**: page number (default 1)
* **pageSize**: number of results in a page (default 10)

Only the walletAddress parameter is required, the rest are optional.

#### Return

Returns an array containing some details of the file(s).

```javascript
[
  {
    source_file_upload_id: <ID>,
    car_file_id: <ID>,
    file_name: <FILE_NAME>,
    file_size: <FILE_SIZE>,
    upload_at: <TIME>,
    duration: 525,
    ipfs_url: <'https://ipfs.multichain.storage/ipfs/Qm...'>,
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
