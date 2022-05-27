---
description: Get Details about a specific file
---

# Get File Details

`getFileDetails(sourceFileUploadId, dealId)`

The following code example gets the file details of an uploaded file. This method takes the upload id of the file, and the deal id of the file. The deal id can be obtained by the getUploads method

```
const SOURCE_FILE_UPLOAD_ID = ''
const DEAL_ID = ''
 
console.log(await mcs.getFileDetails(SOURCE_FILE_UPLOAD_ID, DEAL_ID))
```

### Parameters

* **sourceFileUploadId**: upload id of the file
* **dealId**: deal id of the file

### Return

Returns the response from the `/deal/detail/` API
