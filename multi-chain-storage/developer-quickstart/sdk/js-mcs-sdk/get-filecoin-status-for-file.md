# Get Filecoin Status for File

`getFileStatus(dealId)`

The following code example returns the FIlecoin storage status of a paid file. This method requires the deal id of the deal. This can also be obtained by the getUploads method.

```
const DEAL_ID = 0

const mintResponse = await mcs.getFileStatus(DEAL_ID)
console.log(mintResponse)
```

### Parameters

* **dealId**: deal id of the file

### Return

Returns the response from the `/deal/log/` API
