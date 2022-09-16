---
description: 获取文件的Filecoin存储状态
---

# 获取文件的Filecoin状态

```
getFileStatus(dealId)
```

下面的代码示例返回付费文件的 FIlecoin 存储状态。此方法需要交易的成交 ID。这也可以通过 getUploads 方法获得。

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
  const DEAL_ID = 0
  
  const mintResponse = await mcs.getFileStatus(DEAL_ID)
  console.log(mintResponse)
}

main()
```

#### 参数 <a href="#can-shu-4" id="can-shu-4"></a>

* **dealId**： 文件的 deal id

#### 返回 <a href="#fan-hui-5" id="fan-hui-5"></a>

返回来自 `/deal/log/` API 的响应

```
{
  status: 'success',
  data: {
    offline_deal_log: [ [Object], [Object], [Object], [Object], [Object], [Object] ]
  }
}
```
