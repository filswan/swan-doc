# SDK User Case

## **Introduction** <a href="#sdkusercase-introduction" id="sdkusercase-introduction"></a>

Please refer to [https://docs.filswan.com/multi-chain-storage/overview#introduction](https://docs.filswan.com/multi-chain-storage/overview#introduction)

### **What is MCS Client?** <a href="#sdkusercase-whatismcsclient" id="sdkusercase-whatismcsclient"></a>

MCS Client is a client library for the Multi-Chain Storage (MCS) service. Providing a convenient Javascript interface for developers working with the MCS API from Node.js.&#x20;

* **Zero Cost, Free to Use**
* **Access by Wallet (Metamask)**
* **Seamless Integration, Easy to Implement**

### **Accessibility** <a href="#sdkusercase-accessibility" id="sdkusercase-accessibility"></a>

There are many ways to use the Multi-Chain Service:

* User Interface - [https://mcs.filswan.com/](https://mcs.filswan.com)
* API - [https://docs.filswan.com/development-resource/mcp-api](https://docs.filswan.com/development-resource/mcp-api)
* Javascript SDK - [https://github.com/filswan/js-mcs-sdk](https://github.com/filswan/js-mcs-sdk)

## **Development** <a href="#sdkusercase-development" id="sdkusercase-development"></a>

### **Prerequisites**  <a href="#sdkusercase-prerequisites" id="sdkusercase-prerequisites"></a>

* Node.js, NPM
* MCS Client \`npm install mcs-client\`
* Metamask Private Key, Mumbai RPC URL

### **Getting Started** <a href="#sdkusercase-gettingstarted" id="sdkusercase-gettingstarted"></a>

API guide: [https://docs.filswan.com/development-resource/mcp-api](https://docs.filswan.com/development-resource/mcp-api)

MCS Client Getting Started: [https://github.com/filswan/js-mcs-sdk#usage](https://github.com/filswan/js-mcs-sdk#usage)

### **SDK Methods** <a href="#sdkusercase-sdkmethods" id="sdkusercase-sdkmethods"></a>

#### **Supported API Methods** <a href="#sdkusercase-supportedapimethods" id="sdkusercase-supportedapimethods"></a>

The list below documents the SDK's currently supported MCS API methods

* Upload
* Make Payment
* MintAsset
* ListUploads
* GetFileDetails
* Check Status

### **MCS Client Setup** <a href="#sdkusercase-mcsclientsetup" id="sdkusercase-mcsclientsetup"></a>

After installation, you can create a new client instance using your wallet's private key and an RPC URL. You can obtain an RPC URL from [https://www.alchemy.com/](https://www.alchemy.com)

<details>

<summary>Expand source</summary>

```
const { mcsClient } = require('mcs-client')


const client = new mcsClient({
  privateKey: process.env.PRIVATE_KEY,
  rpcUrl: process.env.RPC_URL,
}) 
```

</details>

### **Uploading Files** <a href="#sdkusercase-uploadingafile" id="sdkusercase-uploadingafile"></a>

The following code example uploads a file, the upload method takes in an array of objects containing fileName and file for file contents.

* fileName: Name of the file
* file: contents of the file

An optional object can also be passed to specify certain parameters:

* delay: delay in milliseconds between upload API calls. Default is 1000, but may need to be increased for many larger files
* duration: 180. The number of days to store your file on the Filecoin network.
* fileType: 0. Files of type one will be hidden from the upload list and the UI. NFT metadata files are type 1.

Returns an array of the upload API responses

<details>

<summary>Expand source</summary>

```
const fileArray = [
  { fileName: 'file1', file: fs.createReadStream('./file1.txt') },
  { fileName: 'file2', file: fs.createReadStream('./file2.txt') },
]

//optional, showing default options
const options = { delay: 1000,  duration: 180,  fileType: 0 }

const uploadResponses = await client.upload(fileArray, options)
console.log(uploadResponses)
```

</details>

### **Making a Payment** <a href="#sdkusercase-makingapayment" id="sdkusercase-makingapayment"></a>

The following code example makes a payment for a file by its payload\_cid. The method takes the payload\_cid as the first parameter and the minimum amount as the second.

* payloadCid: payload\_cid of the file
* amount: minimum amount to pay for the file. String value to avoid Big Number precision errors.

Returns a web3.js receipt object

<details>

<summary> Expand source</summary>

```
const PAYLOAD_CID = ''
const MIN_AMOUNT

const tx = await client.makePayment(PAYLOAD_CID, MIN_AMOUNT)
console.log(tx.transactionHash)
```

</details>

### **Minting Asset** <a href="#sdkusercase-mintingasset" id="sdkusercase-mintingasset"></a>

The following code example mints an uploaded file as a NFT viewable on Opensea. Create an NFT object and provide the payload\_cid of the file. The NFT object follows the Opensea metadata guidelines. \*Required properties

* name\*: The name of your NFT
* image\*: The IPFS URL of your file
* description: The description of your NFT
* attributes: Array of attribute objects you wish to show on Opensea

Returns the response from the mint/info API

<details>

<summary>Expand source</summary>

```
const PAYLOAD_CID = ''
const IPFS_URL = ''

const nft = {
  name: 'NFT NAME', // the name of your NFT
  image: IPFS_URL, // asset URI, images will render on Opensea
}

const mintTx = await client.mintAsset(PAYLOAD_CID, nft)
console.log(mintTx)
```

</details>

### **List Uploaded Files** <a href="#sdkusercase-listuploadedfiles" id="sdkusercase-listuploadedfiles"></a>

The following code example lists a user's uploaded files. The list can also be searched by payload\_cid or file name.

* walletAddress\*: lists the files uploaded by this user
* payloadCid: search for this payload\_cid
* fileName: search by this file name
* pageNumber: page number
* pageSize: number of results in a page

Returns an array containing some details of the file(s).

<details>

<summary>Expand source</summary>

```
console.log(await client.listUploads())


console.log(await client.listUploads(client.publicKey, payloadCid)) // search by payload cid
console.log(await client.listUploads(client.publicKey, '', 'fileName') // search by file name
```

</details>

### **Get File Details** <a href="#sdkusercase-getfiledetails" id="sdkusercase-getfiledetails"></a>

The following code example gets the file details of an uploaded file. This method takes the payload\_cid of the file and the deal\_id of the file. The deal\_id can be obtained by the listUploads method

* payload Cid\*: The payload\_cid of the file
* dealId\*: The deal\_id of the file

Returns the response from the deal/detail/ API

<details>

<summary>Expand source</summary>

```
const PAYLOAD_CID = ''
const DEAL_ID = ''

console.log(await client.getFileDetails(PAYLOAD_CID, DEAL_ID))
```

</details>

### **Check Filecoin Status of File** <a href="#sdkusercase-checkfilecoinstatusoffile" id="sdkusercase-checkfilecoinstatusoffile"></a>

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal\_cid of the deal. This can also be obtained by the listUploads method.

* dealCid\*: deal cid of the file

Returns the response from the deal/log/ API

<details>

<summary> Expand source</summary>

```
const PAYLOAD_CID = ''

// search for file info to get deal_cid
const uploadInfo = await client.listUploads(client.publicKey, PAYLOAD_CID)
const dealCid = uploadInfo.data[0].deal_cid

// not every file will have a deal cid available
if (dealCid) {
  const fileStatus = await client.checkStatus(dealCid)
  console.log(fileStatus)
 } else {
  console.log('deal_cid not found')
}
```

</details>

## **Additional Resources** <a href="#sdkusercase-additionalresources" id="sdkusercase-additionalresources"></a>

### **What is Filecoin?** <a href="#sdkusercase-whatisfilecoin" id="sdkusercase-whatisfilecoin"></a>

[https://docs.filecoin.io/about-filecoin/what-is-filecoin/](https://docs.filecoin.io/about-filecoin/what-is-filecoin/)

### **What is an NFT?** <a href="#sdkusercase-whatisannft" id="sdkusercase-whatisannft"></a>

[https://support.opensea.io/hc/en-us/articles/360063450733-What-is-a-Non-Fungible-Token-NFT-](https://support.opensea.io/hc/en-us/articles/360063450733-What-is-a-Non-Fungible-Token-NFT-)

\
