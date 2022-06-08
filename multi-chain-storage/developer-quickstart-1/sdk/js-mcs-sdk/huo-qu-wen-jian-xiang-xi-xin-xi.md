---
description: 获取有关特定文件的详细信息
---

# 获取文件详细信息

``

```
getFileDetails(sourceFileUploadId, dealId)
```

下面的代码示例获取上载的文件的文件详细信息。此方法获取文件的上传 ID 和文件的交易 ID。交易 ID 可以通过 getUploads 方法获取

```
const SOURCE_FILE_UPLOAD_ID = ''
const DEAL_ID = ''
 
console.log(await mcs.getFileDetails(SOURCE_FILE_UPLOAD_ID, DEAL_ID))
```

#### 参数 <a href="#can-shu-3" id="can-shu-3"></a>

* **sourceFileUploadId**：文件的上传 ID
* **dealId**： 文件的 deal id

#### 返回 <a href="#fan-hui-4" id="fan-hui-4"></a>

返回来自 `/deal/detail/` API 的响应
