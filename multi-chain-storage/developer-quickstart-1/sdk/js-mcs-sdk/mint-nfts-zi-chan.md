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
const SOURCE_FILE_UPLOAD_ID = ''
const IPFS_URL = ''
 
const nft = {
  name: 'NFT NAME', // the name of your NFT
  image: IPFS_URL, // asset URI, images will render on Opensea
  description: 'NFT DESCRIPTION', // description of your NFT
  attributes: [], // NFT attributes displayed on Opensea
}
 
const mintTx = await mcs.mintAsset(SOURCE_FILE_UPLOAD_ID, nft)
console.log(mintTx)
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
