---
description: 使用 MCS SDK 将文件上传到 MCS
---

# 上传文件

```shell
upload(fileArray, options)
```

您可以使用上传功能将文件数组上传到 FilSwan IPFS 网关。该数组保存对象列表，并返回响应对象数组。使用 `fs` 是读取文件数据的简单方法。选项对象也是自定义上载的可选对象。

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
  const PATH_1 = ''
  const PATH_2 = ''
  
  const fileArray = [
    { fileName: 'file1', file: fs.createReadStream(PATH_1) },
    { fileName: 'file2', file: fs.createReadStream(PATH_2) },
  ]
  
  //optional, showing default options
  const options = {
    delay: 1000, // delay between upload API calls for each file. May need to be raised for larger files
    duration: 525, // the number of days to store the file on the Filecoin network.
    fileType: 0, // set to 1 for nft metadata files. type 1 files will not show on the UI.
  }
  
  const uploadResponses = await mcs.upload(fileArray, options)
  console.log(uploadResponses)
}

main()
```

#### 参数 <a href="#can-shu" id="can-shu"></a>

* **fileArray**： 对象数组
  * **fileName**：文件名
  * **file**：文件内容（使用`fs`是获取文件内容的简单方法）
* **options**：还可以传递可选对象以指定某些参数：
  * **delay**：上传 API 调用之间的延迟（以毫秒为单位）。默认值为 1000，但对于许多较大的文件，可能需要增加
  * **duration**：在Filecoin网络上存储文件的天数。（默认值 525）
  * **fileType**：类型为一的文件将从上传列表和 UI 中隐藏。NFT 元数据文件的类型为 1。（默认值 0）

#### 返回 <a href="#fan-hui" id="fan-hui"></a>

此函数返回上载 API 响应的数组。

```
[
  {
    status: 'success',
    data: {
      source_file_upload_id: <ID>,
      payload_cid: <'Qm...'>,
      ipfs_url: <'https://calibration-ipfs.filswan.com/ipfs/Qm...'>,
      file_size: <FILE_SIZE>,
      w_cid: <UNIQUE_CID>
    }
  }, ...
]
```
